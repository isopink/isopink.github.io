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

In conclusion, this problem can be solved in three steps, each called a layer in neural networks. Since the data flows forward only, it forms a feedforward structure. Also, because more layers are used between the input and output to implement $f$ compared to a single perceptron, we call it a multilayer perceptron (MLP). It can solve problems that a single perceptron cannot. For example, a circle can’t be represented by a single line, but we can approximate it using multiple perceptrons to form polygon shapes. This situation is illustrated below:

![solution](/assets/images/nn_6.svg)

The more perceptrons we use, the closer we get to the target shape. However, adding more perceptrons increases the number of weights and the model’s complexity, which makes generalization harder and optimization more difficult. Once you fix the size of the MLP, you learn the weights on every link by fitting the data. Let’s consider the single perceptron:

<br>

$$
h(\mathbf{x}) = \theta(\mathbf{w}^\top \mathbf{x}).
$$

<br>

When using $\theta(s) = \text{sign}(s)$, learning the weights is difficult because the sign function is not smooth. This makes optimization hard, especially in MLPs. To address this, we use a smooth approximation like $\tanh(x)$ instead of $\text{sign}(x)$. We compare those functions as below: 

![solution](/assets/images/nn_7.svg)

The $\tanh$ function is nearly linear near $0$ and saturates at ±1 for large inputs. This makes it a good substitute and is related to the sigmoid function used in logistic regression. Networks using such smooth activation functions are called *sigmoidal neural networks*. In neural networks, the number of weights increases compared to a perceptron, so we need a more precise notation. 

<br>

##### 1.2. Notation 

![solution](/assets/images/nn_8.svg)

Layers are labeled by $\ell = 0, 1, \dots, L$. Each layer $\ell$ contains $d^{(\ell)}$ regular nodes and one bias node (index $0$), which always outputs $1$. We use superscript $^{(\ell)}$ to indicate layer index. The bias node is similar to the convention $x_0 = 1$ in linear models. A neural network is defined by its layer sizes $\mathbf{d} = [d^{(0)}, d^{(1)}, \dots, d^{(L)}]$, where $d^{(\ell)}$ is the number of (non-bias) nodes in layer $\ell$. A specific model $h$ is chosen by setting the weights between layers. 

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

<br>

##### 2.1. Mathematical Insight

We studied an algorithm for getting to a local minimum of a smooth $E_{\text{in}}$ [before](https://isopink.github.io/Linear-Model-ll/), Gradient Descent. Especially, we are going to use Stochastic Gradient Descent (SGD) here, because of the benefits of computation. 

To learn all parameters **w**, we use one data point $(\mathbf{x}_n, y_n)$ at a time. The error at this point is defined as $\mathbf{e}(\mathbf{w})$. To implement stochastic gradient descent, we need to compute the gradient of $\mathbf{e}(\mathbf{w})$, and since we must update all parameter values, this must be done for all layers $l$, and for every $j$ and $i$. To summarzie, we need to find: 

<br>

$$
\nabla \mathbf{e}(\mathbf{w}) 
= \frac{\partial \, \mathbf{e}(\mathbf{w})}{\partial \, w^{(l)}_{ij}} 
\quad \text{for all } i, j, l
$$

<br>

Before we begin, we introduce the senstivity vector $\delta^{(l)}_j$: 

<br>

$$
\delta^{(l)}_j = \frac{\partial \, \mathbf{e}(\mathbf{w})}{\partial \, s^{(l)}_j}
$$

<br>

To begin, let us take a closer look at the partial derivative. The situiation is illustrated in the following figure. 

![solution](/assets/images/nn_12.svg)

The error $\mathbf{e}$ is influenced through a chain from $W^{(\ell)}$ to $\mathbf{x}^{(L)}$ as below: 

<br>

$$
\mathbf{W}^{(\ell)} \rightarrow \mathbf{s}^{(\ell)} \rightarrow \mathbf{x}^{(\ell)} \rightarrow \mathbf{s}^{(\ell+1)} \rightarrow \cdots \rightarrow \mathbf{x}^{(L)} = \mathbf{h}
$$

<br>

We now apply the chain rule for a single weight $w^{(\ell)}_{ij}$, which only affects $s^{(\ell)}_j$. By the chain rule, 

<br>

$$
\frac{\partial \, \mathbf{e}}{\partial \, w^{(\ell)}_{ij}} 
= \frac{\partial \, s^{(\ell)}_j}{\partial \, w^{(\ell)}_{ij}} \cdot 
\frac{\partial \, \mathbf{e}}{\partial \, s^{(\ell)}_j} 
= x^{(\ell - 1)}_i \cdot \delta^{(\ell)}_j
$$

<br>

The last equality follows by definition of $\delta^{(\ell)}_j$ and the weighted sum of $s^{(\ell)}_j$,

<br>

$$
\mathbf{s}^{(\ell)}_j = \sum_{\alpha = 0}^{d^{(\ell - 1)}} w^{(\ell)}_{\alpha j} \, \mathbf{x}^{(\ell - 1)}_\alpha
$$

<br>

Since $\mathbf{e}$ depends on $s^{(\ell)}$ only through $\mathbf{x}^{(\ell)}$, by the chain rule, we have: 

<br>

$$
\delta^{(\ell)}_j 
= \frac{\partial \, \mathbf{e}}{\partial \, s^{(\ell)}_j} 
= \frac{\partial \, \mathbf{e}}{\partial \, \mathbf{x}^{(\ell)}_j} 
\cdot \frac{\partial \, \mathbf{x}^{(\ell)}_j}{\partial \, s^{(\ell)}_j}
$$

<br>

And it can be rewritten as: 

<br>

$$
\theta'\left(s^{(\ell)}_j\right) \cdot \frac{\partial \, \mathbf{e}}{\partial \, \mathbf{x}^{(\ell)}_j}
$$

<br>

To get the partial derivative $\partial \mathbf{e} / \partial \mathbf{x}^{(\ell)}$, we need to understand how $\mathbf{e}$ changes due to changes in $\mathbf{x}^{(\ell)}$. Also, change in $\mathbf{x}^{(\ell)}$ only affects $\mathbf{s}^{(\ell+1)}$ and hence $\mathbf{e}$. Because a particular component of $\mathbf{x}^{(\ell)}$ can affect every component of $\mathbf{s}^{(\ell+1)}$, we need to sum these dependencies using the chain rule:

<br>

$$
\frac{\partial \, \mathbf{e}}{\partial \, \mathbf{x}^{(\ell)}_j} 
= \sum_{k=1}^{d^{(\ell+1)}} 
\frac{\partial \, s^{(\ell+1)}_k}{\partial \, \mathbf{x}^{(\ell)}_j} 
\cdot \frac{\partial \, \mathbf{e}}{\partial \, s^{(\ell+1)}_k}
$$

<br>

And it can be rewritten as: 

<br>

$$
\sum_{k=1}^{d^{(\ell+1)}} w^{(\ell+1)}_{jk} \, \delta^{(\ell+1)}_k
$$

<br>

Putting all this together, we get the final form: 

<br>

$$
\delta^{(\ell)}_j 
= \theta'\left(s^{(\ell)}_j\right) 
\sum_{k=1}^{d^{(\ell+1)}} w^{(\ell+1)}_{jk} \, \delta^{(\ell+1)}_k


$$

<br>

By forward-propagation, we can compute all $\mathbf{x}^{(\ell)}_j$. By backward-propagation, we can compute all $\delta^{(\ell)}_j$. In conclusion, we can compute: 

<br>

$$
\nabla \mathbf{e}(\mathbf{w}) = \frac{\partial \, \mathbf{e}}{\partial \, w^{(\ell)}_{ij}} 
= x^{(\ell - 1)}_i \cdot \delta^{(\ell)}_j
$$

<br>

This is the end. And here is the summary of Backpropagation algorithm. 

<br>

<div style="border:1px solid #ccc; padding:10px; border-radius:6px">

1. Initialize all weights \( w^{(\ell)}_{ij} \) <span style="color:green"><b>at random</b></span>. <br>
2. For \( t = 0, 1, 2, \dots \) do <br>
3.  Pick \( n \in \{1, 2, \cdots, N\} \). <br>
4.  <span style="color:blue"><i>Forward:</i></span> Compute all \( x^{(\ell)}_j \). <br>
5.  <span style="color:red"><i>Backward:</i></span> Compute all \( \delta^{(\ell)}_j \). <br>
6.  Update the weights:  
<br>

$$
w^{(\ell)}_{ij} \leftarrow w^{(\ell)}_{ij} - \eta \, \nabla \mathbf{e}_n(\mathbf{w})
$$

<br>
7.  Iterate to the next step until it is time to stop. <br>
8. Return the final weights \( w^{(\ell)}_{ij} \).

</div>

<br>

##### 2.2. Initialization 

If weights are too large, neuron outputs can saturate and gradients vanish, stopping learning. Zero initialization also fails since all neurons behave the same. Using small random weights keeps neurons responsive and allows gradients to flow. A common method is Gaussian initialization with small variance.

<br>

##### 2.3. Termination 

Small gradients don't always mean learning is done — it could be a flat region. A better rule is to stop when the error is low, changes are small, and a max number of iterations is reached. 

So far, we hgave discussed the backpropagation algorithm as well as initialization and termination. Then, how should we adjust the number of hidden layers or nodes to train properly? This question will be addressed during next three sessions, The Overfitting. 
