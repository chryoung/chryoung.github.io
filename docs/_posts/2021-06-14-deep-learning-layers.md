---
title: Deep Learning -- Layers and Activation Functions
tags: deep-learning
math: true
---

## Notation

$$
a^{[1](2)}
$$

The number in the square ($[1]$ in the equation) indicates the number of the layer. i.e. $[1]$ means the 1st layer.

The number in the parenthesis ($(2)$ in the equation) indicates the number of the training set. i.e. $(2)$ mean the 2nd training set.

## Fully Connected Layers

### Structure

Input layer -> Hidden layers -> Output layer

_The reason the hidden layer got its name is that you should not see the value of it._

### Illustration

<p align="center">
  <img alt="Fully connected layers illustration" src="{% link /assets/deep-learning/fully-connected-layers-render.svg %}" />
</p>
### Equation

#### Single Training Set

$$
\begin{align*}
z & = W \bar{x} + b \\

\hat{y} & = a = \sigma(z)
\end{align*}
$$

where

- $z$ is the value before activation.
- $W$ is the weight.
- $b$ is the bias.
- $\bar{x}$ is the input.
- $\hat{y}$ is the output.
- $a$ is the activation.
- $\sigma(z)$ is the sigmoid activation function.

Take a matrix  $M$ of $(4,3)$ and vector $\bar{x}$ of $(3,1)$ for example

$$
\begin{align*}
\begin{bmatrix}
w_{1,1}^{[1]} w_{1,2}^{[1]} w_{1,3}^{[1]} \\
w_{2,1}^{[1]} w_{2,2}^{[1]} w_{2,3}^{[1]} \\
w_{3,1}^{[1]} w_{3,2}^{[1]} w_{3,3}^{[1]} \\
w_{4,1}^{[1]} w_{4,2}^{[1]} w_{4,3}^{[1]} \\
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
x_3
\end{bmatrix}
+
\begin{bmatrix}
b_1 \\
b_2 \\
b_3 \\
b_4 \\
\end{bmatrix}
=
\begin{bmatrix}
z_1 \\
z_2 \\
z_3 \\
z_4 \\
\end{bmatrix}
\end{align*}
$$

$$
\hat{y} = a = \sigma \left(
\begin{bmatrix}
z_1 \\
z_2 \\
z_3 \\
z_4
\end{bmatrix}
\right)
$$

#### Vectorization for Multiple Training Set

For multiple training sets, we can let the matrix $X$ be

$$
\begin{align*}
X & = [ \bar{x}^{(1)}, \bar{x}^{(2)}, \ldots, \bar{x}^{(n)} ] \\
& =
\begin{bmatrix}
x_1^{(1)} x_1^{(2)} \ldots x_1^{(n)} \\
x_2^{(1)} x_2^{(2)} \ldots x_2^{(n)} \\
\vdots \\
x_n^{(1)} x_n^{(2)} \ldots x_n^{(n)} \\
\end{bmatrix}
\end{align*}
$$

Then for the 1st layer there is

$$
\begin{align*}
Z^{[1]} & = W^{[1]}X + b^{[1]} \\
A^{[1]} & = \sigma(Z^{[1]}) \\
\end{align*}
$$

And the 2nd layer there is

$$
\begin{align*}
Z^{[2]} & = W^{[2]}A^{[1]} + b^{[2]} \\
A^{[2]} & = \sigma(Z^{[2]}) \\
\end{align*}
$$

## Activation Functions

#### tanh

$$
\begin{align*}
\tanh(z) & = \frac{e^z - e^{-z}}{e^z + e^{-z}} \\
\tanh'(z) & = \left[ \frac{e^z - e^{-z}}{e^z + e^{-z}} \right]' = 1 - [\tanh(z)]^2
\end{align*}
$$

<p align="center">
  <img alt="tanh" src="{% link /assets/deep-learning/tanh.svg %}" />
</p>

$tanh$ is preferred in the hidden layer.

#### Sigmoid

$$
\begin{align*}
\sigma(z) & = \frac{1}{1 + e^{-z}} \\
\sigma '(z) & = \sigma(z) (1 - \sigma(z))
\end{align*}
$$

<p align="center">
  <img alt="Sigmoid" src="{% link /assets/deep-learning/sigmoid.svg %}" />
</p>

Sigmoid is preferred in the output layer.

#### ReLu

$$
\begin{align*}
g(z) & = \max(0, z) \\
g'(z) & =
    \begin{cases}
        0, & \text{if}\ z < 0 \\
        1, & \text{if}\ z > 0 \\
        \text{undef}, & \text{if}\ z = 0 \\
    \end{cases}
\end{align*}
$$

<p align="center">
  <img alt="ReLu" src="{% link /assets/deep-learning/relu.svg %}" />
</p>

On the origin $(0, 0) $, $g(z)$ is not differentiable nor derivable.

#### Leaky ReLu

$$
\begin{align*}
g(z) & = \max(0.01z, z) \\
g'(z) & =
	\begin{cases}
		0.01, & \text{if}\ z < 0 \\
		1, & \text{if}\ z \ge 0
	\end{cases}
\end{align*}
$$

<p align="center">
  <img alt="Leaky ReLu" src="{% link /assets/deep-learning/leaky_relu.svg %}" />
</p>

#### Why Activation Function is Needed

If we use id function $g(z) = z$, it will end up with $Wx + b$, a trivial linear function.

But this linear function can be used on output layer like house price.

## Copyright

This post is written by chryoung. You can copy/paste if you cite the source.
