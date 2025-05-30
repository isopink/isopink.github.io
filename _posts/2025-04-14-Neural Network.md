---
layout: single
title: "Lecture 10 : Neural Network"
---

In this time, We will take our first look at neural network. The discussion will proceed in the following two parts: 

1. Neural Network model

2. Backpropagation algorithm.

---

#### 1. Neural Network model

Neural network is made up of many perceptrons, just like a biological neural network is composed of many neurons. We begin with the basic properties of neural networks, and how to train them on data. 

![solution](/assets/images/nn_1.svg) 

The perceptron is simple and useful, but it cannot solve problems that need more than one line to separate classes. For example, if the $+$ and $–$ are split diagonally, single line is not enough. So, we came up with a new idea: use two lines, like $h_1$ and $h_2$, and combine them to solve the problem.

The target $f$ equals $+1$ when exactly one of $h_1, h_2$ equals $+1$. This is the Boolean XOR function:

<br>

$$f = \text{XOR}(h_1, h_2)$$, 

<br>

where $+1$ represents “TRUE” and $-1$ represents “FALSE”. We can rewrite $f$ using the simpler OR and AND operations: $\text{OR}(h_1, h_2) = +1$ if at least one of $h_1, h_2$ equal $+1$ and $\text{AND}(h_1, h_2) = +1$ if both $h_1, h_2$ equal $+1$. Using standard Boolean notation: 

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

A node sends its output through an arrow, which multiplies it by a weight. The next node sums all incoming values and applies the signal function to produce the final output. With this inspection, Our target function $f$ can be illusted as below. 

![solution](/assets/images/nn_3.svg) 

Since the two inputs $\overline{h_1}h_2$ and $h_1\overline{h_2}$ are ANDs, We can illustrate is as below. 

![solution](/assets/images/nn_4.svg) 

Finally, since $h_1 = \text{sign}(\mathbf{w}_1^\top \mathbf{x})$ and $h_2 = \text{sign}(\mathbf{w}_2^\top \mathbf{x})$, we can expand our previous illustration as: 

![solution](/assets/images/nn_5.svg) 

This problem can be solved in three steps, each called a *layer* in neural networks. Since the data flows forward only, it forms a *feed-forward* structure. Also, more layers of nodes are used between the input and output to implement $f$, as compared to the single perceptron, we call it a multilayer - layer perceptron (MLP).

![solution](/assets/images/nn_6.svg)

Neural networks can solve problems that a single perceptron cannot. For example, a circle can’t be represented by one line, but we can approximate it using multiple perceptrons to form polygon shapes. The more perceptrons we use, the closer we get to the target shape. However, adding more perceptrons increases the number of weights and the model’s complexity, which makes generalization harder and optimization more difficult.

![solution](/assets/images/nn_6.svg)

Once you fix the size of the MLP, you learn the weights on every link by fitting the data. Let’s consider the single perceptron:

$$
h(\mathbf{x}) = \theta(\mathbf{w}^\top \mathbf{x}).
$$

When using $\theta(s) = \text{sign}(s)$, learning the weights is difficult because the sign function is not smooth. This makes optimization hard, especially in MLPs. To address this, we use a smooth approximation like $\tanh(x)$ instead of $\text{sign}(x)$.

![solution](/assets/images/nn_7.svg)

The $\tanh$ function is nearly linear near $0$ and saturates at ±1 for large inputs. This makes it a good substitute and is related to the sigmoid function used in logistic regression. Networks using such smooth activation functions are called *sigmoidal neural networks*. 



| 항목             | 기호                         | 설명 |
|------------------|-------------------------------|------|
| Layer index       | $\ell = 0, 1, \dots, L$        | $\ell = 0$: 입력층, $\ell = L$: 출력층, 중간은 은닉층 |
| 노드 개수         | $d^{(\ell)}$                   | layer $\ell$의 노드 수 (bias 제외) |
| 입력 신호 벡터    | $\mathbf{s}^{(\ell)}$          | layer $\ell$에 들어오는 신호 ($d^{(\ell)}$ 차원) |
| 출력 벡터         | $\mathbf{x}^{(\ell)}$          | layer $\ell$의 출력 벡터 <br>($d^{(\ell)} + 1$차원; bias 포함) |
| weight (스칼라)   | $w_{ij}^{(\ell)}$              | layer $\ell - 1$의 노드 $i$ → layer $\ell$의 노드 $j$ 로 가는 weight |
| weight (행렬)     | $\mathbf{W}^{(\ell)}$          | layer $\ell - 1$ → layer $\ell$ 의 가중치 행렬 <br>크기: $(d^{(\ell-1)} + 1) \times d^{(\ell)}$ |
| 전체 가중치 집합  | $\mathbf{w}$                   | $\{\mathbf{W}^{(1)}, \mathbf{W}^{(2)}, \dots, \mathbf{W}^{(L)}\}$ |
| 활성화 함수       | $\theta(s)$                    | 예: $\tanh(s)$, $\text{sign}(s)$ 등 |
| 출력 함수         | $h(\mathbf{x}; \mathbf{w})$    | 전체 네트워크의 출력 함수 |

