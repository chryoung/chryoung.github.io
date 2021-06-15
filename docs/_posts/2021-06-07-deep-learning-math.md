---
layout: post
title: Deep Learning -- Math
tags: deep-learning math
math: true
---

## Math basic

### Matrix Differential

Let

$$
\begin{align*}
dz^{(i)} & = a^{(i)} - y^{(i)} \\
dz & = A - Y = [a^{(i)} - y^{(i)}]
\end{align*}
$$

Since

$$
\begin{align*}
z  & = w^T + b \\
A  & = \sigma(z) \\
dz & = A - Y\\
dw & = \frac{1}{m}xdz^T \\
db & = \frac{1}{m}\sum{dz} \\
\end{align*}
$$

we can know that

$$
\begin{align*}
w & := w - \alpha dw \\
b & := b - \alpha db
\end{align*}
$$

### Loss function

#### Cross entropy loss function

$$
L = -y\log{\hat{y}} - (1 - y)\log{(1 - \hat{y})}
$$

The goal of the machine learning is to minimize the loss function $L$.

#### The deduction of cross entropy

We need a conditional probability function $P$ of $x, y$. And $P$ should satisfy

$$
\begin{align*}
P(y|x) & = \hat{y} & y = 1 \\
P(y|x) & = 1 - \hat{y} & y = 0
\end{align*}
$$

We can see that this function

$$
P(y|x) = \hat{y}^y (1 - \hat{y})^{(1 - y)}
$$

satisfy the condition. If we apply $\log$ to it, then

$$
L = \log{P(y|x)} = -y\log{\hat{y}} - (1 - y)\log{(1 - \hat{y})}
$$

which is the cross entropy.

#### The feature of the cross entropy

When $y = 1$, if $L$ gets less, $-\log{\hat{y}}$ gets less too, while $\log{\hat{y}}$ gets greater. So that $\hat{y} < 1$. Because the $\log$ is applied to $\hat{y}$, when $\log{\hat{y}}$ is close to $\infty$, $\hat{y}$ is close to 1.

When $y = 0$, and $\log{(1 - \hat{y})}$ is close to $- \infty$, $\hat{y}$ is close to 0.

Our goal is to let $\hat{y} \to y$. Because minimizing $L$ will make $\hat{y} \to y$.

#### Jacobi determinant

$$
J(w, b) = \frac{1}{m}\sum_{i = 1}^{m} L(\hat{y}^{(i)}, y^{(i)})
$$

Let $A = \sigma(w^TX +b)$, its partial derivative is

$$
\begin{align*}
\frac{\partial J}{\partial w} & = \frac{1}{m} X (A - Y)^T \\
\frac{\partial J}{\partial b} & = \frac{1}{m} \sum_{(i = 1)}^m (a^{(i)} - y^{(i)})
\end{align*}
$$

#### L1 Loss, L2 Loss

L1 Loss

$$
L1 = \sum_{(i = 0)}^{n} | y^{(i)} - \hat{y}^{(i)} |
$$

L2 Loss

$$
L2 = \sum_{(i = 0)}^{n} ( y^{(i)} - \hat{y}^{(i)} )^2
$$

#### Backpropagation

Definition: Make $\hat{y}$ close to $y$ using the gradient.

<p align="center">
  <img alt="Backward propagation" src="/assets/deep-learning/back-propagation-render.svg" />
</p>


Steps of backward propagation:

1. Forward-propagation: calculate the value of loss $L$
2. Backward-propagation: calculate the gradient of the loss $L$ with respect to parameters
3. Update the parameters using the gradient from step2

### Matrix Multiplication

Take the rows from the left matrix, and the columns from the right matrix, then sum the bit-wise product of the elements.

$$
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
\begin{bmatrix}
5 \\
6
\end{bmatrix}

=

\begin{bmatrix}
17 \\
39
\end{bmatrix}
$$

The number of rows is equal to the one of the left matrix, while the number of columns is equal to the one of the right matrix.

### Data cleaning

**Centralize:** Subtract the average of the samples from every sample.  e.g. If there are samples $s_1, s_2, ..., s_n$, and their average is $a$, then the centralized data is $s_1 - a, s_2 - a, ..., s_n - a$.

Steps for cleaning the new data:

1. Figure out the shape and the dimension of the data
2. Reshape
3. Standardize

## Numpy Functions

```python
np.zeros((n, 1)) # create a matrix of size (n, 1) filled with 0
np.dot(x, y) # dot product of x and y
np.sum(dz) # sum of the matrix dz
np.array(a) # convert python array a to numpy array
```

$$z = w^T x + b$$ is `z = np.dot(wT, x) + b` in numpy.

Avoid using rank 1 array.

## Copyright

This post is written by chryoung. You can copy/paste if you cite the source.
