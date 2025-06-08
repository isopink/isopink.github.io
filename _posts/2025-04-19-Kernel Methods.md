---
layout: single
title: "Lecture 15 : Kernel Methods"
---

In this time, we are going to discuss the Kernel methods to deal with the nonlinear transformations. The discussion will proceed in the following two parts: 

1. Kernel Trick

2. Soft-margin SVM

--- 

#### 1. Kernel Trick 

We have discussed the nonlinear transformation with applying [SVM](https://isopink.github.io/SVM/). However, when data is transformed into a high-dimensional space ($\mathcal{Z}$ space), linear separation becomes easier, but the computational complexity may increases dramatically. Kernel methods will deal with it.  

Let us first recall what we have done in $\mathcal{Z}$ space. We have: 

<br>

$$
\mathcal{L}(\alpha) = \sum_{n=1}^{N} \alpha_n - \frac{1}{2} \sum_{n=1}^{N} \sum_{m=1}^{N} y_n y_m \alpha_n \alpha_m \, \mathbf{z}_n^\top \mathbf{z}_m
$$

<br>

And the constraints: 

<br>

$$ 
\alpha_n \geq 0 \quad \text{for} \quad n = 1, \cdots, N \\ \\ \sum_{n=1}^{N} \alpha_n y_n = 0
$$  

<br>

We don't see any $\mathbf{z}$ in constraints, however, in forming the Lagrangain, we need the inner product $\mathbf{z}_n^\top \mathbf{z}_m$. After solving Lagrangian, we will get a final hypothesis: 

<br>

$$
g(\mathbf{x}) = \text{sign}(\mathbf{w}^\top \mathbf{z} + b)
$$

<br>

Where, 

$$
\mathbf{w} = \sum_{\mathbf{z}_n \text{ is SV}} \alpha_n y_n \mathbf{z}_n \quad \text{and} \quad y_m(\mathbf{w}^\top \mathbf{z}_m + b) = 1
$$

To compute $\mathbf{w}^\top \mathbf{z} + b$, we need inner product of $\mathbf{z}$ again. 

Both cases, we only deal with $\mathbf{z}$ as the inner product. Then, if we are able to compute the inner product in the $\mathcal{Z}$ space without visiting the $\mathbf{Z}$ space, we can carry this machinery. Let us look at this idea as being a generalized inner product. 


 
