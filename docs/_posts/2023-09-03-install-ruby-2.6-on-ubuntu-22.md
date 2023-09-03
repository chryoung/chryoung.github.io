---
title: Install Ruby 2.6 on Ubuntu 22
tags: ruby ubuntu linux
---

## Compile OpenSSL 1.1

```bash
mkdir ~/lib
cd ~/lib
wget https://www.openssl.org/source/openssl-1.1.1g.tar.gz
tar zxvf openssl-1.1.1g.tar.gz
mv openssl-1.1.1g openssl-1.1.1g-src
cd openssl-1.1.1g-src
./config --prefix=$HOME/lib/openssl-1.1.1g --openssldir=$HOME/lib/openssl-1.1.1g

make
make install

# Link cert
rm -rf ~/lib/openssl-1.1.1g/certs
ln -s /etc/ssl/certs ~/lib/openssl-1.1.1g/certs
```

## Install Ruby using RVM

```bash
rvm install ruby-2.6.10 --with-openssl-dir=$HOME/lib/openssl-1.1.1g
```

## Reference

- [Installing Older Ruby Versions on Ubuntu 22.04](https://deanpcmad.com/2022/installing-older-ruby-versions-on-ubuntu-22-04/)
- [troubles with RVM and OpenSSL](https://stackoverflow.com/questions/15511943/troubles-with-rvm-and-openssl)