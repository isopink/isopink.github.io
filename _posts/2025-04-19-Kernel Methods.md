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
$$

<br>

The interesting thing is that the space is infinite-dimensional. We might worry about generalization performance, however, we don't have to. We just count number of support vectors. So, let us keep going. Above formula can be decomposed into two separate terms: 

<br>

$$
\sqrt{\frac{2^k}{k!}} \exp\left(-\frac{x^2}{2}\right) x^k
$$

<br>

$$
\sqrt{\frac{2^k}{k!}} \exp\left(-\frac{(x')^2}{2}\right) (x')^k 
$$

<br>

We can interpret this as the inner product of transformed vector $\mathbf{x}$ and $\mathbf{x}'$. This is very interesting kernel, called Radial Basis Funtion, which we will discuss next session. It corresponds to an infinite-dimensional space, but we can carry it out by computing a fairly simple exponential between $x$'s. So, let us look at it in action. 

Consider we are given slightly non-separable $100$ data in the $\mathcal{X}$ space as shown below: 

![solution](/assets/images/km_1.svg) 

There is no straight line to separate them. And we lighten the target funtion. We will leave it in order to compare it with the final hypothesis that we get. Now, we are going to transform $\mathcal{X}$ into an infinite-dimensional space. However, all we need is the inner product for QP solver, and QP solver will give us support vectors. So, we will apply kernel method. Let us look at the following figure. 

![solution](/assets/images/km_2.svg) 

We highlighted pre-image of nine support vectors. So to speak, our [upper bound of $E_{\text{out}}$](https://isopink.github.io/SVM/) is at most $0.1$. Now, let us look at the final hypothesis. 

![solution](/assets/images/km_3.svg) 

We can see why support vectors are called support vectors. They are sort of holding the line. We are now fully convinced of the effectiveness of kernel methods. Now, let us examine how to formulate the problem. We already know it, since we have discussed [last time](https://isopink.github.io/SVM/), but just let us take it step by step. Let us recall the previous one: 

<br> 

$$
\frac{1}{2} \boldsymbol{\alpha}^\top \mathbf{Q} \boldsymbol{\alpha} - \mathbf{1}^\top \boldsymbol{\alpha}
$$

<br>

This was the matrix notation of our Lagrangian. And the $N$ by $N$ matrix $Q$ was: 

<br>

$$
\begin{bmatrix}
y_1 y_1 \, \mathbf{z}_1^\top \mathbf{z}_1 & y_1 y_2 \, \mathbf{z}_1^\top \mathbf{z}_2 & \cdots & y_1 y_N \, \mathbf{z}_1^\top \mathbf{z}_N \\
y_2 y_1 \, \mathbf{z}_2^\top \mathbf{z}_1 & y_2 y_2 \, \mathbf{z}_2^\top \mathbf{z}_2 & \cdots & y_2 y_N \, \mathbf{z}_2^\top \mathbf{z}_N \\
\vdots & \vdots & \ddots & \vdots \\
y_N y_1 \, \mathbf{z}_N^\top \mathbf{z}_1 & y_N y_2 \, \mathbf{z}_N^\top \mathbf{z}_2 & \cdots & y_N y_N \, \mathbf{z}_N^\top \mathbf{z}_N
\end{bmatrix}
$$

<br>

Applying kernel method, inner product of $\mathbf{z}$ can be expressed as:

<br>

$$
\mathbf{z}^\top \mathbf{z}' = K(\mathbf{x}, \mathbf{x}')
$$

<br>

This is the only difference so far. Once we pass it to the QP solver, we will obtain the $\alpha$. Now, let us look at the final hypothesis: 

<br>

$$
g(\mathbf{x}) = \text{sign}(\mathbf{w}^\top \mathbf{z} + b) \quad \text{ in terms of } \quad K(\cdot, \cdot)
$$

<br>

We are going to translate it in terms of the kernel by substituting: 

<br>

$$
\mathbf{w} = \sum_{\mathbf{z}_n \text{ is SV}} \alpha_n y_n \mathbf{z}_n
$$

<br>

Then, $g(\mathbf{x})$ can be expressed as: 

<br>

$$
g(\mathbf{x}) = \text{sign} \left( \sum_{\alpha_n > 0} \alpha_n y_n K(\mathbf{x}_n, \mathbf{x}) + b \right)
$$

<br>

Moreover, for any support vector ($\alpha > 0$), we can substitute $b$ by 

<br>

$$
b = y_m - \sum_{\alpha_n > 0} \alpha_n y_n K(\mathbf{x}_n, \mathbf{x}_m)
$$

<br>

We are completely ready here. 

Now, the only problem we have is that we don't know the kernel is valid. There are three approaches. First one is construction, such as the Polynominal Kernel. The second relies on the mathematical properties of kernels, such as Mercer's conditon, Which will be explained soon. The final one is just not to worry about it. Who cares? :> Let us examine the Mercer's condition. 

