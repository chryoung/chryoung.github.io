---
layout: post
title: Deep learning -- Math for Backpropagation
mathjax: true
---

## The Derivative of Cross Entropy Loss Function

Here is the definition of the cross entropy loss function $L$:

$$
L = -y \log \hat{y}  - (1 - y) \log (1 - \hat{y})
$$

Let $\hat{y} = a = wx + b$, there is

$$
\begin{align}
\frac{dL}{d\hat{y}} & = - \frac{y}{\hat{y}} + \frac{1 - y}{1 - \hat{y}} \\
\frac{d\hat{y}}{dw} & = x \\
\frac{d\hat{y}}{db} & = 1
\end{align}
$$

So we can know that the partial derivative of $L$ with respect to $w$ is

$$
\begin{align}
\frac{\partial{L}}{\partial{w}} & = \frac{dL}{d\hat{y}} \frac{d\hat{y}}{dw} \\
& = -\frac{xy}{\hat{y}} + \frac{x(1 - y)}{1 - \hat{y}}
\end{align}
$$

and the partial derivative of $L$ with respect to $b$ is

$$
\begin{align}
\frac{\partial{L}}{\partial{b}} & = \frac{dL}{d\hat{y}} \frac{d\hat{y}}{db}\\
& = - \frac{y}{\hat{y}} + \frac{1 - y}{1 - \hat{y}} \\
& = \frac{\hat{y}-y\hat{y} - y + y\hat{y}}{(1-\hat{y})\hat{y}} \\
& = \frac{\hat{y} - y}{\hat{y} - \hat{y}^2} \\
& = \frac{1}{1- \hat{y}} - \frac{y}{\hat{y}(1 - \hat{y})}
\end{align}
$$

and the partial derivative of $L$ with respect to $z$ is

$$
\begin{align}
\frac{\partial{L}}{\partial{z}} & = \frac{dL}{da} \frac{da}{dz} \\
& = \left(-\frac{y}{a} + \frac{1 - y}{1 - a} \right) \left( \frac{1}{1 + e^{-z}} \right)' \\
& = \left(-\frac{y}{a} + \frac{1 - y}{1 - a} \right)  (a (1 - a)) \\
& = -y ( 1 - a) + a (1 - y) \\
& = -y + ay + a - ay \\
& = a - y
\end{align}
$$

## The Derivative of Sigmoid Function

Definition:

$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$

Let

$$
f(x) = \frac{1}{\sigma(x)} = 1 + e^{-x}
$$

then

$$
\begin{align}
f'(x) & = -e^{-x} = \frac{d\left[ \frac{1}{\sigma(x)} \right]}{dx} \\
& = [\sigma(x)^{-1}]' \\
& = -\sigma(x)^{-2} \sigma ' (x) \\
& = - \frac{\sigma '(x)}{\sigma (x)^2}
\end{align}
$$

Since

$$
-e^{-x} = f'(x) = 1 - f(x) = 1 - \frac{1}{\sigma (x)} = \frac{\sigma (x) - 1}{\sigma (x)}
$$

there is

$$
\begin{align}
- \frac{\sigma '(x)}{\sigma (x)^2} & = \frac{\sigma (x) - 1}{\sigma (x)} \\
\sigma' (x) & = \frac{1 - \sigma(x)}{\sigma (x)} \sigma (x)^2 \\
& = \sigma (x) (1 - \sigma (x))
\end{align}
$$

## Copyright

This post is written by chryoung. You can copy/paste if you cite the source.
