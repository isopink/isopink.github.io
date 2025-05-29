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

When we encounter 'non' seperable data set, transforming input vectors $x$'s to $z$ in $z$-space, called feature transform is a classical way to deal with it. However, there is a price we have to pay. Transforming data to make it linearly separable usually increases the dimensionality, which raises the VC dimension and makes generalization harder. Sometimes, feature transform may not be a good idea. Let me introduce two examples.

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

After seeing that the learned result resembled a circle, why don't we intentionally reduce the dimensionality of the transformed data? The term $x_1$, $x_2$ and $x_1 x_2$ seems useless! 
