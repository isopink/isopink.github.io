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

Last time we talked about gradeient descent. It is a good method to find optimal weights $\mathcal{w}$. However, We are forced to use whole $N$ data points every iterative steps, updating the gradient. This approach of processing all the data at once for a single update is called batch. So far, we have discussed the Batch Gradient Descent (BGD). 
