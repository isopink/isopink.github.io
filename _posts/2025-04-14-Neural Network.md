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

Since the two inputs 
