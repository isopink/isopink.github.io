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

In this section, we derive a regularization method that applies to a wide variety of learning problems. To simplify the math, we will use the concrete setting of regression using Legendre polynomials, the polynomials of increasing complexity. Let us first formally introduce you to the Legendre polynomials.

<br>

##### 3.1. Legendre polynominal

Legendre polynomials are a standard set of polynomials with nice analytic properties that result in simpler derivations. The zeroth-order Legendre polynomial is the constant $L_0(x) = 1$, and the first few Legendre polynomials are illustrated below.

![solution](/assets/images/rr_4.svg) 

As you can see, when the order of the Legendre polynomial increases, the curve gets more complex. Legendre polynomials are orthogonal to each other within $x \in [-1, 1]$, and any regular polynomial can be written as a linear combination of Legendre polynomials, just like it can be written as a linear combination of powers of $x$. 

<br>

##### 3.2. The polynominal model 

Polynomial models are a special case of linear models in a space $\mathcal{Z}$, under a nonlinear transformation $\Phi : \mathcal{X} \rightarrow \mathcal{Z}$.  
Here, for the $Q$th order polynomial model, $\Phi$ transforms $x$ into a vector $\mathbf{z}$ of Legendre polynomials,

<br>
$$
\mathbf{z} =
\begin{bmatrix}
1 \\
L_1(x) \\
\vdots \\
L_Q(x)
\end{bmatrix}.
$$
<br>

Our hypothesis set $\mathcal{H}_Q$ is a linear combination of these polynomials:

<br>
$$
\mathcal{H}_Q = \left\{ h \;\middle|\; h(x) = \mathbf{w}^\top \mathbf{z} = \sum_{q=0}^{Q} w_q L_q(x) \right\}, \quad \mathbf{w} \in \mathbb{R}^{Q+1},
$$
<br>

where $L_0(x) = 1$. As usual, we will sometimes refer to the hypothesis $h$ by its weight vector $\mathbf{w}$.  
Since each $h$ is linear in $\mathbf{w}$, we can use the machinery of linear regression from [Lecture 3](https://isopink.github.io/Linear-Model-L/) to minimize the squared error:

<br>
$$
E_{\text{in}}(\mathbf{w}) = \frac{1}{N} \sum_{n=1}^{N} (\mathbf{w}^\top \mathbf{z}_n - y_n)^2. \tag{4.2}
$$
<br>

We can write it down with matrix notation as: 



The case of polynomial regression with squared-error measure illustrates the main ideas of regularization well, and facilitates a solid mathematical derivation.  
Nonetheless, our discussion will generalize in practice to non-linear, multi-dimensional settings with more general error measures.  
The baseline algorithm (without regularization) is to minimize $E_{\text{in}}$ over the hypotheses in $\mathcal{H}_Q$ to produce the final hypothesis  
$g(x) = \mathbf{w}_{\text{in}}^\top \mathbf{z}$, where $\mathbf{w}_{\text{in}} = \arg\min_{\mathbf{w}} E_{\text{in}}(\mathbf{w})$.



