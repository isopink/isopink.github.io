---
layout: single
title: "Lecture 10 : Neural Network"
---

In this time, we will revisit and elaborate on some aspects of gradient descent discussed in the [previous time](https://isopink.github.io/Linear-Model-ll/). We will also take our first look at neural network. The discussion will proceed in the following three parts: 

1. Stochastic gradient descent

2. Neural network model

3. Backpropagation algorithm.

---

#### 1. Stochastic gradient descent

The version of gradient descent we have described so far is known as *batch* gradient descent(BGD) – the gradient is computed for the error on the whole data set before a weight update is done. A sequential version of gradient descent known as *stochastic gradient descent* (SGD) turns out to be very efficient in practice.  
Instead of considering the full batch batch gradient on all $N$ training data points, we consider a stochastic version of the gradient. 

First, Pick a random training point $(x_n, y_n)$ and update the model using only its error. This randomness is why it's called *stochastic*. And consider only the error on that data point. In the case of logistic regression, 

<br>

$$
e_n(\mathbf{w}) = \ln \left( 1 + e^{-y_n \, \mathbf{w}^\top \mathbf{x}_n} \right)
$$

<br>

and the weight updata is, 

$$
\mathbf{w(t+1)} = \mathbf{w(t)} - \eta \nabla e_n(\mathbf{w})
$$

Since the data is picked uniformly at random from $\{1, \ldots, N\}$, the expected weight change is: 

<br>

$$
\mathbb{E}_n \left[ -\nabla \mathbf{e}\left(\mathbf{w}\right) \right] = \frac{1}{N} \sum_{n=1}^{N} -\nabla \mathbf{e}\left(\mathbf{w}\right)
$$

<br>

SGD behaves like batch gradient descent on average, though it's noisier due to randomness. Over time, these fluctuations cancel out. There are some advantages of SGD. One major advantage of SGD is its faster computation. Unlike batch gradient descent, which uses all data points to compute the gradient, SGD uses only one data point per update, making each step much quicker.  

![solution](/assets/images/nn_1.svg) 

Another benefit is its randomness, which helps escape local minima. Real-world loss surfaces are often bumpy, and SGD's noisy updates give it a chance to jump out of bad spots and find better solutions. 

