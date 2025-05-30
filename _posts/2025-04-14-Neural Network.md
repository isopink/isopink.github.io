---
layout: single
title: "Lecture 10 : Neural Network"
---

This time, we will take our first look at neural networks.  
The discussion will proceed in two parts:

1. Neural network model  
2. Backpropagation algorithm

---

#### 1. Neural Network Model

A neural network is made up of many perceptrons, just like a biological neural network is composed of many neurons.  
We begin by introducing the basic structure of neural networks and how to train them on data.

![solution](/assets/images/nn_1.svg) 

The perceptron is simple and useful, but it cannot solve problems that require more than one line to separate the classes.  
For example, if the $+$ and $–$ symbols are split diagonally, a single line is not enough.  
So, we came up with a new idea: use two lines, like $h_1$ and $h_2$, and combine them to solve the problem.

The target $f$ equals $+1$ when exactly one of $h_1$ or $h_2$ equals $+1$.  
This is the Boolean XOR function:

<br>

$$f = \text{XOR}(h_1, h_2)$$

<br>

Here, $+1$ represents “TRUE” and $-1$ represents “FALSE”.  
We can rewrite $f$ using simpler OR and AND operations:  
$\text{OR}(h_1, h_2) = +1$ if at least one of $h_1$, $h_2$ equals $+1$,  
and $\text{AND}(h_1, h_2) = +1$ if both equal $+1$.  
Using standard Boolean notation:

<br>

$$
f = h_1\overline{h_2} + \overline{h_1}h_2
$$

<br>

OR and AND can be implemented using perceptrons:

<br>

$$
\text{OR}(x_1, x_2) = \text{sign}(x_1 + x_2 + 1.5)
$$  

<br>

$$
\text{AND}(x_1, x_2) = \text{sign}(x_1 + x_2 - 1.5)
$$

<br>

This can be illustrated as follows:

![solution](/assets/images/nn_2.svg) 

Each node sends its output through an arrow, which multiplies it by a weight.  
The next node sums all incoming values and applies the activation function to produce the final output.  
Based on this, our target function $f$ can be illustrated as:

![solution](/assets/images/nn_3.svg) 

Since the two inputs $\overline{h_1}h_2$ and $h_1\overline{h_2}$ are ANDs,  
we can illustrate them as:

![solution](/assets/images/nn_4.svg) 

Finally, since $h_1 = \text{sign}(\mathbf{w}_1^\top \mathbf{x})$ and $h_2 = \text{sign}(\mathbf{w}_2^\top \mathbf{x})$,  
we can expand our previous illustration as:

![solution](/assets/images/nn_5.svg) 

This problem can be solved in three steps, each called a *layer* in neural networks.  
Since the data flows only forward, this forms a *feedforward* structure.  
Because more layers are used between input and output compared to a single perceptron,  
we call this a multilayer perceptron (MLP).

![solution](/assets/images/nn_6.svg)

Neural networks can solve problems that a single perceptron cannot.  
For example, a circle cannot be represented by a straight line,  
but we can approximate it using multiple perceptrons to form a polygon.  
The more perceptrons we use, the closer we get to the target shape.  
However, using more perceptrons also increases the number of weights and model complexity,  
which makes generalization harder and optimization more difficult.

![solution](/assets/images/nn_6.svg)

Once you fix the size of the MLP, you train it by learning the weights on each connection using the data.  
Let’s consider a simple perceptron:

$$
h(\mathbf{x}) = \theta(\mathbf{w}^\top \mathbf{x})
$$

When using $\theta(s) = \text{sign}(s)$, it's difficult to learn the weights  
because the sign function is not smooth. This makes optimization especially hard in MLPs.  
To solve this, we use a smooth function like $\tanh(x)$ instead of $\text{sign}(x)$.

![solution](/assets/images/nn_7.svg)

The $\tanh$ function is almost linear near $0$ and saturates at ±1 for large inputs.  
This makes it a good replacement and closely related to the sigmoid function used in logistic regression.  
Networks that use such smooth activation functions are called *sigmoidal neural networks*.  

In neural networks, the number of weights is much larger than in a single perceptron,  
so we need more precise notation.

![solution](/assets/images/nn_8.svg)

Layers are labeled as $\ell = 0, 1, \dots, L$.  
Each layer $\ell$ contains $d^{(\ell)}$ regular nodes and one bias node (index $0$), which always outputs $1$.  
We use the superscript $^{(\ell)}$ to indicate the layer.  
The bias node is similar to the convention $x_0 = 1$ in linear models.  

A neural network is defined by its layer sizes:  
$\mathbf{d} = [d^{(0)}, d^{(1)}, \dots, d^{(L)}]$,  
where $d^{(\ell)}$ is the number of non-bias nodes in layer $\ell$.  
A specific model $h$ is formed by choosing the weights between layers.

![solution](/assets/images/nn_9.svg)

Each node receives an input $s$ and produces an output $x$.  
Connections between layers are represented by weights $w_{ij}^{(\ell)}$,  
which connect node $i$ in layer $\ell-1$ to node $j$ in layer $\ell$.  
Each layer also includes a bias node (index $0$) that always outputs $1$.  
The input layer passes input values directly and has no incoming weights.

![solution](/assets/images/nn_10.svg)

To compute values layer by layer, we use vector and matrix notation.  
The input signals to nodes $1, \dots, d^{(\ell)}$ in layer $\ell$ are collected into a vector $\mathbf{s}^{(\ell)}$.  
The outputs from nodes $0, \dots, d^{(\ell)}$, including the bias node, are collected in $\mathbf{x}^{(\ell)}$.  

Each layer $\ell$ has a weight matrix $\mathbf{W}^{(\ell)}$ of size $(d^{(\ell-1)} + 1) \times d^{(\ell)}$.  
The $(i, j)$-entry of $\mathbf{W}^{(\ell)}$ is $w_{ij}^{(\ell)}$,  
which connects node $i$ in the previous layer to node $j$ in layer $\ell$.  
Here is a summary:

<br>

| Item         | Symbol              | Description                                  |
|--------------|---------------------|----------------------------------------------|
| signals in   | $\mathbf{s}^{(\ell)}$     | $d^{(\ell)}$-dimensional input vector         |
| outputs      | $\mathbf{x}^{(\ell)}$     | $(d^{(\ell)} + 1)$-dimensional output vector (includes bias) |
| weights in   | $\mathbf{W}^{(\ell)}$     | $(d^{(\ell-1)} + 1) \times d^{(\ell)}$ dimensional matrix |
| weights out  | $\mathbf{W}^{(\ell+1)}$   | $(d^{(\ell)} + 1) \times d^{(\ell+1)}$ dimensional matrix |

<br>
