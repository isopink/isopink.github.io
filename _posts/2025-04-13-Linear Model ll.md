---
layout: single
title: "Lecture 9 : The Linear Model II"
---

In this time, We will discuss the rest of [Linear Model](https://isopink.github.io/Linear-Model-L/). The discussion will proceed in the following three parts:

1. Review of Nonlinear transforms

2. Logistic Regression

3. Error measure of Logistic Regression

4. Learning algorithm of Logistic Regression

---

#### 1. Review of nonlinear transforms 

We studied nonlinear transformations in [Lecture 3](https://isopink.github.io/Linear-Model-L/), but we didn’t cover everything. Therefore, we would like to add a few more points about nonlinear transformations. 

![solution](/assets/images/lm_1.svg) 

When data isn’t linearly separable, we often apply a feature transform to map $x$ to $z$-space. But this increases dimensionality, raising the VC dimension and making generalization harder. So, it’s not always a good idea. Let’s look at two examples.

![solution](/assets/images/lm_2.svg) 

<br>

##### 1.1. Case 1

The first case offers two choices: accept some $E_\text{in}$ with a linear model, or transform to a higher dimension to make the error zero. 

![solution](/assets/images/lm_3.svg) 

We can clearly recognize that transform to a higher-dimension is a disaster. We cannot gerneralize it well. By accepting some $E_\text{in}$, we can generalize it well. 

<br>

##### 1.2. Case 2

![solution](/assets/images/lm_4.svg) 

The second case is definitely non separable. There is no choice but to transform to a higher-dimension. We can think of all possible quadratic curves in $\mathcal{X}$ and describe this feature transform $z=\Phi$ as: 

<br>

$$ \Phi_2(\mathbf{x}) = (1, x_1, x_2, x_1^2, x_1 x_2, x_2^2) $$

<br>

After seeing the result looks like a circle, it’s tempting to remove terms like $x_1$, $x_2$, and $x_1 x_2$ to reduce the VC dimension. But we must not — that’s data snooping. It uses future information and leads to overfitting and poor generalization.

Feature transform is powerful tool. However, with inspection of case $1$ and $2$, It is not always useful tool. The generalization woudl impossible. We have to choose $\Phi$ carefully. 

---

#### 2. Logistic Regression

The core of the linear model is the 'signal' $ s = \mathbf{w}^\mathrm{T} \mathbf{x} $. We have seen two models based on this signal, and we are now going to introduce a third. In Logistic Regression, the signal is converted into a probability through the formula $theta$:

<br> 

$$ 
\theta(s) = \frac{e^s}{1 + e^s} 
$$ 

<br> 

It is a type of sigmoid function. As $s$ increase, $theta(s)$ approaches $1$, and as $s$ decreases, $theta(s) approaches $0$. Let us consider a concrete example. To predict heart attacks, a linear classifier gives only yes or no. But since risk isn't deterministic, logistic regression is better. It outputs the probability $\theta(s)$, where $s$ is a linear risk score — higher $s$ means higher risk.


