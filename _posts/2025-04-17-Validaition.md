---
layout: single
title: "Lecture 13 : Validation"
---

In this time, we will discuss **validation**, a powerful and practical tool to estimate $E_{\text{out}}$ and control overfitting. The discussion will proceed in the following three parts:

1. The validation set
2. Model selection  
3. Cross-validation  

---

#### 1. The validation set 

Let us contrast validation with regularization first, when overfitting is concerned. $E_{\text{out}}$ can be expressed as below: 

<br>

$$
E_{\text{out}}(h) = E_{\text{in}}(h) + \text{overfit penalty}
$$

<br>

This tells us that $E_{\text{in}}$ is not exactly $E_{\text{out}}$. The more complex the model, the bigger the overfit penalty. So, what does regularizaiton do? 

<br>

$$
E_{\text{out}}(h) = E_{\text{in}}(h) + \underbrace{\text{overfit penalty}}_{\text{regularization estimates this quantity}}
$$

<br>

Regularizaiton tried to guess overfit penalty. Basically, we made up a term that we think represents the overfitting penalty. Now, to constrast this, What does validation do? 

<br>

$$
\underbrace{E_{\text{out}}(h)}_{\text{validation estimates this quantity}} = E_{\text{in}}(h) + \text{overfit penalty}
$$

<br>

Validation estimates $E_{\text{out}}$ directly. This is not completely a foreign idea to us, because we use a test set in order to do that. Let us stpend a few moment to describe the estimate. 

Consider we are given an out-of-sample point, $(\mathbf{x},y)$. We used to call it test point. Now, we are going to call it validation point. It won't be clear why we are naming it differently until we use the validation set later. We represent our error as:  

<br>

$$
e(h(\mathbf{x}), y)
$$

<br>

This could be a simple squared error, or binary error. We have seen these before. Now, if we take this qunatity as: 

<br>

$$
\mathbb{E} \left[ e(h(\mathbf{x}), y) \right] = E_{\text{out}}(h)
$$

<br>

This is an unbiased estimate of $E_{\text{out}}$ as its expected value over the distribution on $mathbf{x}$ is simply $E_{\text{out}}$. And, the variance is: 

<br>

$$
\mathrm{Var} \left[ e(h(\mathbf{x}), y) \right] = \sigma^2
$$

<br>

We denote the variance as $\sigma^2$. However, since we are using only one point, the estimate will be poor. Therefore, we cannot rely on it to estimate $E_{\text{out}}$. To get around this issue, let us move on to a full set. 

 ![solution](/assets/images/nn_1.svg) 


