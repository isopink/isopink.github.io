---
layout: single
title: "Lecture 10 : Neural Network"
---

This time, we will take our first look at neural networks. The discussion will proceed in the following two parts: 

1. Neural network model  
2. Backpropagation algorithm.

---

#### 1. Neural Network model

A neural network is made up of many perceptrons, just like a biological neural network is composed of many neurons. We begin with the basic properties of neural networks, and how to train them on data. 

<br>

##### 1.1. Multilayer perceptron

![solution](/assets/images/nn_1.svg) 

The perceptron is simple and useful, but it cannot solve problems that need more than one line to separate classes. For example, if the $+$ and $–$ are split diagonally, a single line is not enough. So, we came up with a new idea: use two lines, like $h_1$ and $h_2$, and combine them to solve the problem.

The target $f$ equals $+1$ when exactly one of $h_1, h_2$ equals $+1$. This is the Boolean XOR function:

<br>

$$f = \text{XOR}(h_1, h_2)$$

<br>

We can rewrite $f$ using the simpler OR and AND operations. Using standard Boolean notation: 

<br>

$$
f = h_1\overline{h_2} + \overline{h_1}h_2.
$$

<br>

OR and AND can be implemented by the perceptron: 

<br>

$$
\text{OR}(x_1, x_2) = \text{sign}(x_1 + x_2 + 1.5)
$$  

<br>

$$
\text{AND}(x_1, x_2) = \text{sign}(x_1 + x_2 - 1.5)
$$

<br>

This can be illustrated as below. 

![solution](/assets/images/nn_2.svg) 

A node sends its output through an arrow, which multiplies it by a weight. The next node sums all incoming values and applies the sign function to produce the final output. With this in mind, our target function $f$ can be illustrated as below. 

![solution](/assets/images/nn_3.svg) 

Since the two inputs $\overline{h_1}h_2$ and $h_1\overline{h_2}$ are ANDs, we can illustrate them as below. 

![solution](/assets/images/nn_4.svg) 

Finally, since $h_1 = \text{sign}(\mathbf{w}_1^\top \mathbf{x})$ and $h_2 = \text{sign}(\mathbf{w}_2^\top \mathbf{x})$, we can expand our previous illustration as: 

![solution](/assets/images/nn_5.svg) 

This problem can be solved in three steps, each called a *layer* in neural networks. Since the data flows forward only, it forms a *feedforward* structure. Also, because more layers are used between the input and output to implement $f$ compared to a single perceptron, we call it a multilayer perceptron (MLP).

![solution](/assets/images/nn_6.svg)

Neural networks can solve problems that a single perceptron cannot. For example, a circle can’t be represented by a single line, but we can approximate it using multiple perceptrons to form polygon shapes. The more perceptrons we use, the closer we get to the target shape. However, adding more perceptrons increases the number of weights and the model’s complexity, which makes generalization harder and optimization more difficult.

![solution](/assets/images/nn_6.svg)

Once you fix the size of the MLP, you learn the weights on every link by fitting the data. Let’s consider the single perceptron:

$$
h(\mathbf{x}) = \theta(\mathbf{w}^\top \mathbf{x}).
$$

When using $\theta(s) = \text{sign}(s)$, learning the weights is difficult because the sign function is not smooth. This makes optimization hard, especially in MLPs. To address this, we use a smooth approximation like $\tanh(x)$ instead of $\text{sign}(x)$.

![solution](/assets/images/nn_7.svg)

The $\tanh$ function is nearly linear near $0$ and saturates at ±1 for large inputs. This makes it a good substitute and is related to the sigmoid function used in logistic regression. Networks using such smooth activation functions are called *sigmoidal neural networks*. In neural networks, the number of weights increases compared to a perceptron, so we need a more precise notation. 

<br>

##### 1.2. Notation 

![solution](/assets/images/nn_8.svg)

Layers are labeled by $\ell = 0, 1, \dots, L$. Each layer $\ell$ contains $d^{(\ell)}$ regular nodes and one bias node (index $0$), which always outputs $1$.

We use superscript $^{(\ell)}$ to indicate layer index. The bias node is similar to the convention $x_0 = 1$ in linear models. A neural network is defined by its layer sizes $\mathbf{d} = [d^{(0)}, d^{(1)}, \dots, d^{(L)}]$, where $d^{(\ell)}$ is the number of (non-bias) nodes in layer $\ell$. A specific model $h$ is chosen by setting the weights between layers. 

![solution](/assets/images/nn_9.svg)

Each node receives an input $s$ and produces an output $x$. Connections between layers are defined by weights $w_{ij}^{(\ell)}$, which go from node $i$ in layer $\ell-1$ to node $j$ in layer $\ell$. Every layer includes a bias node (index $0$) that always outputs $1$. The input layer only passes input values and does not receive any weights.

![solution](/assets/images/nn_10.svg)

To work with the network layer by layer, we use vector and matrix notation. The input signals to nodes $1, \dots, d^{(\ell)}$ in layer $\ell$ are collected in the vector $\mathbf{s}^{(\ell)}$. The outputs from nodes $0, \dots, d^{(\ell)}$, including the bias node, are collected in $\mathbf{x}^{(\ell)}$.

Each layer $\ell$ has a weight matrix $\mathbf{W}^{(\ell)}$ of size $(d^{(\ell-1)} + 1) \times d^{(\ell)}$. The $(i, j)$-entry of $\mathbf{W}^{(\ell)}$ is $w_{ij}^{(\ell)}$.

<br>

| Item         | Symbol              | Description                                  |
|--------------|---------------------|----------------------------------------------|
| signals in   | $\mathbf{s}^{(\ell)}$     | $d^{(\ell)}$-dimensional input vector         |
| outputs      | $\mathbf{x}^{(\ell)}$     | $(d^{(\ell)} + 1)$-dimensional output vector (includes bias) |
| weights in   | $\mathbf{W}^{(\ell)}$     | $(d^{(\ell-1)} + 1) \times d^{(\ell)}$ dimensional matrix |
| weights out  | $\mathbf{W}^{(\ell+1)}$   | $(d^{(\ell)} + 1) \times d^{(\ell+1)}$ dimensional matrix |

<br>
