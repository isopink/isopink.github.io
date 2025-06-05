---
layout: single
title: "Lecture 12 : Regularization"
---

In this time, we will introduce regularization, a kind of way to deal with [overfitting](https://isopink.github.io/Overfitting/). The discussion will proceed in following four parts: 

1. Simple example of regularization. 

2. Regularization : informal

3. Regularization : formal

4. Weight decay

5. Choosing a regularizer

---

#### 1. Simple example of regularization. 

Regularization constratins the learning algorithm to improve $E_{\text{out}}$ expecially when noise is present. Let us recall the previous example, applying very small amount of 'regularization'. 

![solution](/assets/images/rr_1.svg) 

Though we only used a very small 'amount' of regularizaiton, the fit improves dramatically. We can regularize our algotirthm heuristically and mathematically. We will discuss both of them. 

---

#### 2. Regularization : informal 

Regularization can be viewed through the [VC bound](https://isopink.github.io/VC-Dimension/), which penalizes model complexity:

<br>  

$$  
E_{\text{out}}(h) \leq E_{\text{in}}(h) + \Omega(\mathcal{H}) \quad \text{for all } h \in \mathcal{H}
$$  

<br>

So, we are better off if we fit the data using a simple $\mathcal{H}$. Extrapolating one step further, we should be better off by fitting the data using a ‘simple’ $h$ from $\mathcal{H}$. Instead of minimizing $E_{\text{in}}(h)$ alone, one minimizes a combination of $E_{\text{in}}(h)$ and $\Omega(h)$. This avoids overfitting by constraining the learning algorithm to fit the data well using a simple hypothesis. Let us consider a familiar example: 

![solution](/assets/images/rr_2.svg) 

We constrain the weight to fitting the target $f(x) = \sin(\pi x)$ using $N = 2$ data points as we have seen in [Lecture 8](https://isopink.github.io/Bias-and-variance/). We use linear model to fit the target. The $E_{\text{out}}$ in terms of Bias-Variance Decomposition is illustrated below: 

![solution](/assets/images/rr_3.svg) 
 
As expected, the regularized model performs better than the unregularized one. While $\bar{g}(x)$ seem unchanged, the model distribution has narrowed. This slightly increases bias but significantly reduces variance by eliminating out-of-range fits. That is to say, $E_{\text{out}}$ is reduced. 

This example shows why regularization is necessary. The linear model is too complex for the small dataset—it can perfectly fit any two points, leading to overfitting. Regularization helps by accounting for both the quantity and quality of data. Instead of switching to a simpler model like constant functions, we can use the complex model with constraints. This approach gives better flexibility and leads to the best $E_{\text{out}}$.  

---

#### 3. Regularization : formal 





