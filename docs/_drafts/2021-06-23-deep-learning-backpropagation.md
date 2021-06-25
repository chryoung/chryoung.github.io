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

Let the loss function be the cross entropy function, and the activation function be $g(z)$.

$$
\begin{align*}
dA^{[0]} & = & -\frac{Y}{\hat{Y}} - \frac{1 - Y}{1 - \hat{Y}} \\
& \vdots & \\
dZ^{[i]} & = & g'(z)dA^{[i]} \\
dW^{[i]} & = & dZ^{[i]} \cdot A^{[i-1]} \\
db^{[i]} & = & \sum^{n}_{i = 0} dZ^{[i]}_{i} \\
dA^{[i-1]} & = & W^{[i]} \cdot dZ^{[i]}
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
