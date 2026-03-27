---
title: Install CachyOS on Surface Laptop with Window Dual Boot
tags: os dual-boot
---

Dual-booting a Surface device is a battle against Microsoft’s firmware locking. If you follow a standard guide, you'll end up in an endless UEFI boot loop. After days of "suffer-testing," here is the definitive "Golden Path" to getting CachyOS running alongside Windows 11 with Secure Boot Enabled.

## 1. The Prerequisites (The "Clean Slate" Strategy)

Standard Surface partitions are far too small for dual-booting with signed kernels, and BitLocker often interferes with the installation process. We start with a total wipe.

### A. Manual Windows Installation & EFI Setup

To ensure we have enough space for Secure Boot signatures and multiple Linux kernels, we manually create a **1GB EFI partition** during the Windows installation.

1. Boot from your Windows 11 USB.
2. At the "Language Selection" screen, press **Shift + F10** to open the Command Prompt.
3. Run the following `diskpart` commands:

```bash
diskpart

# Identify your NVMe drive (usually Disk 0)
list disk

# Select your main drive
select disk 0

# WARNING: This wipes the entire drive!
clean

# Convert to GPT for UEFI compatibility
convert gpt

# Create a 1GB EFI Partition (Standard is only 100MB)
create partition efi size=1024
format quick fs=fat32 label="System"

# Create the required Microsoft Reserved Partition
create partition msr size=16

# Create the Windows partition using 400gib. Left around 599gib for CachyOS on a 1T SSD
create partition primary size=409600
format quick fs=ntfs label="Windows"

exit
```

1. Continue the Windows installation. When asked where to install, choose the large Primary partition you just created.

### B. Firmware Preparation

Before moving to the Linux installation:

**Disable Secure Boot:** Enter the Surface UEFI (Volume Up + Power) and set Secure Boot to None.

**Disable BitLocker:** Ensure Device Encryption is turned OFF in Windows settings to allow Linux to see the drive partitions.

### C. The Intune Factor

If your Surface is managed by your organization (Intune/Company Portal), do not enroll the device until after your CachyOS installation is finished and stable. Enrolling too early may force-enable BitLocker and lock your partition table.

## 2. The Installation

* OS: CachyOS (Arch-based).
* Filesystem: ext4 for the root partition (Avoid BTRFS subvolumes to simplify the bootloader path).
* Mounting:
  * Windows EFI (1GB) -> /boot/efi
  * Linux Root -> /
  * Must: **8GB** FAT32 partition for /boot.

## 3. Installing the Linux-Surface Kernel

Standard kernels lack touch/keyboard drivers for Surface. We need the community kernel.
Add the Repository:

```bash
# Import keys
curl -s https://raw.githubusercontent.com/linux-surface/linux-surface/master/pkg/keys/surface.asc | sudo pacman-key --add -
sudo pacman-key --finger 56C464BAAC421453
sudo pacman-key --lsign-key 56C464BAAC421453

# Add to /etc/pacman.conf
# Add these lines to the end of the file:
# [linux-surface]
# Server = https://pkg.surfacelinux.com/arch/

Install Kernel & Drivers:
sudo pacman -Syu
sudo pacman -S linux-surface linux-surface-headers iptsd
```

(Note: Skip the linux-surface-secureboot-mok package. We are using the superior sbctl method.)

## 4. Mastering Secure Boot with sbctl

Instead of using a clunky Microsoft-signed "Shim," we are taking ownership of the motherboard's keys.

* Enter Setup Mode: In Surface UEFI, delete factory keys/Reset to Setup Mode.
* Enroll Keys:

```bash
sudo sbctl create-keys
sudo sbctl enroll-keys -m  # The -m keeps Microsoft keys so Windows stays bootable!
```

* Sign Everything:

```bash
sudo sbctl sign -s /boot/vmlinuz-linux-surface
sudo sbctl sign -s /boot/vmlinuz-linux-cachyos
sudo sbctl sign -s /boot/efi/EFI/cachyos/grubx64.efi
```

## 5. The "Anti-Lock" GRUB Trick (Crucial)

Surface firmware has a "Shim Lock" policy that triggers a rescue mode if you use custom keys with standard GRUB. You must reinstall GRUB with this flag:

```sh
sudo grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=CachyOS --modules="tpm" --disable-shim-lock --recheck

echo GRUB_DISABLE_OS_PROBER=false | sudo tee /etc/default/grub

sudo grub-mkconfig -o /boot/grub/grub.cfg

sudo sbctl sign-all
```

* Why? This tells GRUB to trust your hardware's sbctl keys instead of looking for a Microsoft "Shim" middleman.

## 6. Verification

Re-enable Secure Boot in the UEFI. It should show as "Enabled (Custom)".

* Result: Windows 11 boots. CachyOS boots with full touch/keyboard support. Intune sees Secure Boot is "On." Sanity restored.
Pro-Tip: There is a pacman hook of sbctl which signs the imagine every time the kernel is updated. You don't have to run `sudo sbctl sign-all` every time.

## Disclaimer

This article is written with the help of AI.
