---
title: Deep Learning -- Backpropagation
tags: deep-learning
math: true
---

## Prerequisite

- [Forward propagation]({% post_url 2021-06-14-deep-learning-layers %})
- [Derivate of activation function]({% post_url 2021-06-14-deep-learning-layers %})
- [Derivate of cross entropy loss function]({% post_url 2021-06-08-deep-learning-backpropagation-math %})

## Backpropagation

### Calculate Differential

Let the loss function $L(\hat\{y\})$ be the cross entropy function, and the activation function be $g(z)$.

$$
\begin{align*}
dA^{[n]} & = & dL = -\frac{Y}{\hat{Y}} - \frac{1 - Y}{1 - \hat{Y}} \\
& \vdots & \\
dZ^{[i]} & = & g'(z)dA^{[i]} \\
dW^{[i]} & = & \frac{dZ^{[i]} \cdot \left( A^{[i-1]} \right) ^ T}{m} \\
db^{[i]} & = & \frac{\sum^{n}_{i = 0} dZ^{[i]}_{i}}{m} \\
dA^{[i-1]} & = & \left( W^{[i]} \right) ^ T \cdot dZ^{[i]}
\end{align*}
$$

where:

- $m$ is the second dimension of $A^\{[i - 1]\}$.
- $n$ is  the total number of the layers.

Suppose we have a deep neural network with 2 layer. The backpropagation will be:

$$
\begin{align*}
dA^{[2]} & = & dL = -\frac{Y}{\hat{Y}} - \frac{1 - Y}{1 - \hat{Y}} \\
dZ^{[2]} & = & g'(z)dA^{[2]} \\
dW^{[2]} & = & \frac{dZ^{[2]} \cdot \left( A^{[1]} \right) ^ T}{m} \\
db^{[2]} & = & \frac{\sum^{n}_{i = 0} dZ^{[2]}_{i}}{m} \\
dA^{[1]} & = & \left( W^{[2]} \right) ^ T \cdot dZ^{[2]} \\
dZ^{[1]} & = & g'(z)dA^{[1]} \\
dW^{[1]} & = & \frac{dZ^{[1]} \cdot \left( A^{[0]} \right) ^ T}{m} \\
db^{[1]} & = & \frac{\sum^{n}_{i = 0} dZ^{[1]}_{i}}{m} \\
dA^{[0]} & = & \left( W^{[1]} \right) ^ T \cdot dZ^{[1]} \\
dZ^{[0]} & = & g'(z)dA^{[0]} \\
dW^{[0]} & = & \frac{dZ^{[0]} \cdot \left( A^{[-1]} \right) ^ T}{m} \\
db^{[0]} & = & \frac{\sum^{n}_{i = 0} dZ^{[0]}_{i}}{m} \\
A^{[-1]} & = & X \\
\end{align*}
$$

### Update Parameters

Update the parameters using

$$
\begin{align*}
W^{[i]} & := & W^{[i]} - \alpha dW^{[i]} \\
b^{[i]} & := & b^{[i]} - \alpha db^{[i]}
\end{align*}
$$

where $\alpha$ is the learning rate.
