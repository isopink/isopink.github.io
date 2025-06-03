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

where $+1$ denotes TRUE, $-1$ denotes FLASE. We can rewrite $f$ using the simpler OR and AND operations. Using standard Boolean notation: 

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

After fixing the weights $ \mathbf{W}^{(\ell)} $ for $ \ell = 1, \dots, L $, we have specified a particular neural network hypothesis $ h \in \mathcal{H}_{\text{nn}} $. We collect all these weight matrices into a single weight parameter: 

<br>

$$ \mathbf{w} = \{ \mathbf{W}^{(1)}, \mathbf{W}^{(2)}, \dots, \mathbf{W}^{(L)} \} $$

<br>

##### 1.3. Forward Propagation 

Observe that the inputs and outputs of a layer are related by the transformation function: 

<br>

$$
\mathbf{x}^{(\ell)} = \begin{bmatrix}
1 \\
\theta(s^{(\ell)})
\end{bmatrix}
$$

<br>

where $ \theta(\mathbf{s}^{(\ell)}) $ is a vector whose components are $ \theta(s_j^{(\ell)}) $. To get the input vector into layer $ \ell $, we compute the weighted sum of the outputs from the previous layer. This process is compactly represented by the matrix equation: 

<br>

$$
\mathbf{s}^{(\ell)} = \left( \mathbf{W}^{(\ell)} \right)^\top \mathbf{x}^{(\ell-1)}
$$

<br>

Initialize input layer to $\mathbf{x}^{(0)} = \mathbf{x}$, and consider following chain: 

<br>

$$
\mathbf{x} = \mathbf{x}^{(0)} 
\xrightarrow{\mathbf{W}^{(1)}} \mathbf{s}^{(1)} 
\xrightarrow{\theta} \mathbf{x}^{(1)} 
\cdots 
\xrightarrow{\theta} \mathbf{x}^{(L)} 
= h(\mathbf{x}).
$$

<br>

Here are the summary figure: 

![solution](/assets/images/nn_11.svg)

If we want to compute $ E_{\text{in}} $, all we need is $ h(\mathbf{x}_n) $ and $ y_n $. For the sum of squares: 

<br>

$$
E_{\text{in}}(\mathbf{w}) 
= \frac{1}{N} \sum_{n=1}^{N} \left( x_n^{(L)} - y_n \right)^2.
$$

<br>

We now discuss how to minimize $E_{\text{in}}$ to obtain the learned weights. 

---

#### 2. Backpropagation Algorithm

We studied an algorithm for getting to a local minimum of a smooth $E_{\text{in}}$ [before](https://isopink.github.io/Linear-Model-ll/), Gradient Descent. Especially, we are going to use Stochastic Gradient Descent (SGD) here, because of the benefits of computation. 

To learn all parameters **w**, we use one data point $(\mathbf{x}_n, y_n)$ at a time. The error at this point is defined as $\mathbf{e}(\mathbf{w})$. To implement stochastic gradient descent, we need to compute the gradient of $\mathbf{e}(\mathbf{w})$, and since we must update all parameter values, this must be done for all layers $l$, and for every $j$ and $i$. To summarzie, we need to find: 

<br>

$$
\nabla \mathbf{e}(\mathbf{w}) : \quad \frac{\partial \, \mathbf{e}(\mathbf{w})}{\partial \, w^{(l)}_{ij}} \quad \text{for all } i, j, l
$$

<br>

We can evaluate $\nabla \mathbf{e}(\mathbf{w})$ one by one, but that's an computational disaster. We now introduce an elegant computation technique, known as Backpropagation. It is based on several applications of the chain rule to write partial derivatives. Consider following figure. 

![solution](/assets/images/nn_12.svg) 

Here is a trick for efficient computation for $\nabla \mathbf{e}(\mathbf{w})$:

<br>

$$
\frac{\partial \, \mathbf{e}(\mathbf{w})}{\partial \, w^{(l)}_{ij}} 
= \frac{\partial \, \mathbf{e}(\mathbf{w})}{\partial \, s^{(l)}_j} 
\times \frac{\partial \, s^{(l)}_j}{\partial \, w^{(l)}_{ij}}
$$

<br>

We have, 

<br>

$$
\frac{\partial \, s^{(l)}_j}{\partial \, w^{(l)}_{ij}} = x^{(l-1)}_i
$$

<br>

We only need the rest of the equation, called, sensitivity vector: 

<br>

$$
\delta^{(l)}_j= \frac{\partial \, \mathbf{e}(\mathbf{w})}{\partial \, s^{(l)}_j}
$$

<br>

Here is the key idea. We can compute $\delta^{(l-1)}_j$ with $\delta^{(l)}_j$. Let the final layer $l = L$ and $j = 1$. And we use the squared error as our error measure. Then, 

<br>

$$
\mathbf{e}(\mathbf{w}) = \left( x^{(L)}_1 - y_n \right)^2
$$

<br>

Since $x^{(L)}_1$ is the output of the activation function $\theta$ and input $s^{(L)}_1$, 

<br>

$$
x^{(L)}_1 = \theta(s^{(L)}_1)
$$

<br>

Furthermore, We use **tanh** as a activation function $\theta$. So, 

<br>

$$
\theta'(s) = 1 - \theta^2(s)
$$

<br>

With these inspections, We compute $\delta^{(l-1)_i)$ as below: 

<br>

$$
\begin{aligned}
\delta^{(l-1)}_i 
&= \frac{\partial \, \mathbf{e}(\mathbf{w})}{\partial \, s^{(l-1)}_i} \\ \\
&= \sum_{j=1}^{d^{(l)}} 
\frac{\partial \, \mathbf{e}(\mathbf{w})}{\partial \, s^{(l)}_j}
\times \frac{\partial \, s^{(l)}_j}{\partial \, x^{(l-1)}_i}
\times \frac{\partial \, x^{(l-1)}_i}{\partial \, s^{(l-1)}_i} \\ \\
&= \sum_{j=1}^{d^{(l)}} 
\delta^{(l)}_j \times w^{(l)}_{ij} \times \theta'(s^{(l-1)}_i) \\ \\
&= \left(1 - \left(x^{(l-1)}_i\right)^2\right)
\sum_{j=1}^{d^{(l)}} w^{(l)}_{ij} \, \delta^{(l)}_j
\end{aligned}
$$

<br>
