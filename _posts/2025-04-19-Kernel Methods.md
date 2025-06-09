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

<br>

$$
\mathbf{w} = \sum_{\mathbf{z}_n \text{ is SV}} \alpha_n y_n \mathbf{z}_n \quad \text{and} \quad y_m(\mathbf{w}^\top \mathbf{z}_m + b) = 1
$$

<br>

To compute $\mathbf{w}^\top \mathbf{z} + b$, we need inner product of $\mathbf{z}$ again. 

Both Lagrangian and hypotehsis, we only deal with $\mathbf{z}$ as the inner product. Then, if we are able to compute the inner product in the $\mathcal{Z}$ space without visiting the $\mathbf{Z}$ space, we can carry this machinery. Let us look at this idea as being a generalized inner product. 

Suppose we are given two points, $\mathbf{x}$ and $\mathbf{x}' \in \mathcal{X}$. We transform them and take an inner product in the $\mathcal{Z}$ space, $\mathbf{z}^\top \mathbf{z}'$. However, we want to treat it as if it was a generalized inner product in the $\mathcal{X}$ space. In other words: 

<br>

$$
\text{Let } \quad \mathbf{z}^\top \mathbf{z}' = K(\mathbf{x}, \mathbf{x}')
$$

<br>

We don't know which funtion, but we know it is a function, Since $\mathbf{z}$ is a funtion of $\mathbf{x}$, being transformed version. We are ging to call this, Kernel. Can we compute this without transforming $\mathbf{x}$ and $\mathbf{x}'$? Let us consider following example: 

<br>

$$
K(\mathbf{x}, \mathbf{x}') = \left(1 + \mathbf{x}^\top \mathbf{x}'\right)^2
$$

<br>

Suppose we are given two-dimensional vector $\mathbf{x}$. So we have two coordinates, $x_1$ and $x_2$. Then the above Kernel can be written as below: 

<br>

$$
\left(1 + x_1 x_1' + x_2 x_2'\right)^2
$$

<br>

Finally, we get this: 

<br>

$$
1 + x_1^2 {x_1'}^2 + x_2^2 {x_2'}^2 + 2 x_1 x_1' + 2 x_2 x_2' + 2 x_1 x_1' x_2 x_2'
$$

<br>

This is the value of the Kernel. It looks like an inner product, except for $2$'s. However, this still is an inner product. We can consider the $\mathbf{x}$ and $\mathbf{x}'$ goes through the following transformation $\Phi$: 

<br>

$$
\Phi(x_1, x_2) = \left( 1,\ x_1^2,\ x_2^2,\ \sqrt{2}x_1,\ \sqrt{2}x_2,\ \sqrt{2}x_1x_2 \right)
$$

<br>

Now, let us introduce the general case, Polynominal Kernel. Consider we are given: 

<br>

$$
\mathcal{X} = \mathbb{R}^d \\ \\
\Phi: \mathcal{X} \rightarrow \mathcal{Z} \ \text{is polynomial of order } Q
$$

<br> 

The Kernel will be: 

<br>

$$
K(\mathbf{x}, \mathbf{x}') = (a \mathbf{x}^\top \mathbf{x}' + b)^Q
$$

<br>

And it can be expanded as below: 

<br>

$$
(1 + x_1 x_1' + x_2 x_2' + \cdots + x_d x_d')^Q
$$

<br>

It is a tremendous number of terms, which are all orders up to $Q$, of different combinations of the $x$'s. It is better to compute $ \mathbf{x}^\top \mathbf{x}'$ and raise it to the power $Q$. It turns out that if we compute inner product in some space $\mathcal{Z}$, everything is okay. We will get support vectors and generalization bound will be guranteed. This is the key idea of our trick. 

So far, we were able to examine what the $\mathcal{Z}$ is. Now, let us try to get a kernel that maps us to $\mathcal{Z}$ without imagining what $\mathcal{Z}$ is. Consider following case: 

<br>

$$
K(\mathbf{x}, \mathbf{x}') = \exp\left( -\gamma \|\mathbf{x} - \mathbf{x}'\|^2 \right)
$$

<br>



It is definitely a funtion of $\mathcal{x}$ and $\mathcal{x}'$. However, it is not clear that we can compute inner product either in $\mathcal{X}$ space or $\mathcal{Z}$ space. 

Our question is, does this actually correspond to some $\mathcal{Z}$ space and inner product in $\mathcal{Z}$ space? Can we get the same number by visiting some space? The answer is yes. To simplify the math, let $\mathcal{X} = \mathbb{R}^1$ and $\gamma = 1$. Then kernel becomes: 

<br>

$$
K(x, x') = \exp\left( - (x - x')^2 \right)
$$

<br>

Now, let us express this using taylor series as below: 

<br>

$$
\exp(-x^2)\exp(-{x'}^2) \sum_{k=0}^{\infty} \frac{2^k (x)^k ({x'})^k}{k!}
\quad \text{(which equals } \exp(2xx') \text{)}
$$

<br>

