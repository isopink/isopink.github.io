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

<br>

##### 1.1. What is Kernel? 

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

We can see why support vectors are called support vectors. They are sort of holding the line. We are now fully convinced of the effectiveness of kernel methods. 

<br>

##### 1.2. Formulate the problem 

Now, let us examine how to formulate the problem. We already know it, since we have discussed [last time](https://isopink.github.io/SVM/), but just let us take it step by step. Let us recall the previous one: 

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

<br>

##### 1.3. Is kernel valid? 

Now, the only problem we have is that we don't know the kernel is valid. There are three approaches to verify. First one is construction, such as the Polynominal Kernel. The second relies on the mathematical properties of kernels, such as Mercer's conditon, Which will be explained soon. The final one is just not to worry about it. Who cares? :> 

Let us introduce the Mercer's condition. Kernel is valid if and only if: 

<br>

$$
K(\mathbf{x}, \mathbf{x}') = K(\mathbf{x}', \mathbf{x}) 
$$ 

<br>

$$
\text{and}
$$

<br>  

$$
\forall N,\, \forall \{\mathbf{x}_1, \dots, \mathbf{x}_N\},\, \mathbf{K} \succeq 0
$$

<br>

where $\mathbf{K}$ is $N$ by $N$ matrix as shown below: 

<br>

$$
\begin{bmatrix}
K(\mathbf{x}_1, \mathbf{x}_1) & K(\mathbf{x}_1, \mathbf{x}_2) & \cdots & K(\mathbf{x}_1, \mathbf{x}_N) \\
K(\mathbf{x}_2, \mathbf{x}_1) & K(\mathbf{x}_2, \mathbf{x}_2) & \cdots & K(\mathbf{x}_2, \mathbf{x}_N) \\
\vdots & \vdots & \ddots & \vdots \\
K(\mathbf{x}_N, \mathbf{x}_1) & K(\mathbf{x}_N, \mathbf{x}_2) & \cdots & K(\mathbf{x}_N, \mathbf{x}_N)
\end{bmatrix}
$$

<br>

--- 

#### 2. Soft-margin SVM

There are two types of non-separable data. First one is seriously non-separable data as illusted in the following figure: 

![solution](/assets/images/km_4.svg) 

We have done this type of problems by using Kernel method. The other one is slightly non-separable data: 

![solution](/assets/images/km_5.svg) 

There are a few outliers, but mapping to a high-dimensional nonlinear space solely to handle them does not seem reasonable. Furthermore, SVM may not be suitable in this case, as it results in an excessive number of support vectors. We now introduce Soft-margin SVM to deal with it. Consider we are given following situation. 

![solution](/assets/images/km_6.svg) 

The current issue lies with data points that violate the margin region between support vectors. So the condition so the constraint $y_n(\mathbf{w}^\top \mathbf{x}_n + b) \geq 1$ does not hold. To handle this issue, we introduce slack variables $xi_n >0$. Then, constraints becomes: 

<br>

$$
y_n(\mathbf{w}^\top \mathbf{x}_n + b) \geq 1 - \xi_n
$$

<br>

And the total violation can be expressed as: 

<br>

$$
\sum_{n=1}^{N} \xi_n
$$

<br>

Since the constraits are changed, our optimization method should be updated as: 

<br>

$$
\text{Minimize} \quad \frac{1}{2} \, \mathbf{w}^\top \mathbf{w} + C \sum_{n=1}^{N} \xi_n
$$

<br>

subject to: 

<br>

$$
y_n(\mathbf{w}^\top \mathbf{x}_n + b) \geq 1 - \xi_n \quad \text{for } n = 1, \dots, N
$$

<br>

$$
\xi_n \geq 0 \quad \text{for } n = 1, \dots, N
$$

<br>

$$
\mathbf{w} \in \mathbb{R}^d,\quad b \in \mathbb{R},\quad \boldsymbol{\xi} \in \mathbb{R}^N
$$

<br>

We are trying to maximize the margin and mimize the error simultaneously. The constant $C$ denotes the relative importance between two terms. Now, let us update our Lagrangian: 

<br>

$$
\begin{aligned}
\mathcal{L}(\mathbf{w}, b, \boldsymbol{\xi}, \boldsymbol{\alpha}, \boldsymbol{\beta}) 
= \; & \frac{1}{2} \, \mathbf{w}^\top \mathbf{w} 
+ C \sum_{n=1}^{N} \xi_n \\
- \; & \sum_{n=1}^{N} \alpha_n \left( y_n(\mathbf{w}^\top \mathbf{x}_n + b) - 1 - \xi_n \right) \\
- \; & \sum_{n=1}^{N} \beta_n \, \xi_n
\end{aligned}
$$

<br>

We are going to minimize Lagrangian with respect to $\mathbf{w}$, $b$, and $\boldsymbol{\xi}$ and maximize with respect to each $\text{each } \alpha_n \geq 0$ and  $\beta_n \geq 0$. Then we get the following equations: 

<br>

$$
\nabla_{\mathbf{w}} \mathcal{L} = \mathbf{w} - \sum_{n=1}^{N} \alpha_n y_n \mathbf{x}_n = 0
$$

<br>

$$
\frac{\partial \mathcal{L}}{\partial b} = - \sum_{n=1}^{N} \alpha_n y_n = 0
$$

<br>

$$
\frac{\partial \mathcal{L}}{\partial \xi_n} = C - \alpha_n - \beta_n = 0
$$

<br>

By substituting, with respect to $\boldsymbol{\alpha}$, we are going to maximize: 

<br>

$$
\sum_{n=1}^{N} \alpha_n 
- \frac{1}{2} \sum_{n=1}^{N} \sum_{m=1}^{N} 
y_n y_m \, \alpha_n \alpha_m \, \mathbf{x}_n^\top \mathbf{x}_m
$$

<br>

Subject to: 

<br>

$$
0 \leq \alpha_n \leq C \quad \text{for } n = 1, \dots, N
\quad \text{and} \quad
\sum_{n=1}^{N} \alpha_n y_n = 0
$$

<br>

Then, QP solver will give us $\mathbf{w}$: 

<br>

$$
\mathbf{w} = \sum_{n=1}^{N} \alpha_n y_n \mathbf{x}_n
$$

<br>

which minimizes: 

<br>

$$
\text{minimizes} \quad \frac{1}{2} \, \mathbf{w}^\top \mathbf{w} + C \sum_{n=1}^{N} \xi_n
$$

<br>

We are done. Now, let us discuss the two types of support vectors. 

<br>

| Type                     | Range                        | Constraints                                  | Slack Variable         |
|:------------------------:|:----------------------------:|:--------------------------------------------:|:----------------------:|
| Margin support vector    | $ 0 < \alpha_n < C $         | $ y_n(\mathbf{w}^\top \mathbf{x}_n + b) = 1 $ | $ \xi_n = 0 $          |
| Non-margin support vector| $ \alpha_n = C $             | $ y_n(\mathbf{w}^\top \mathbf{x}_n + b) < 1 $ | $ \xi_n > 0 $          |


<br>

Unlike before, not all support vectors lie on the margin. According to the modified condition, if $\xi_n = 0$, the support vector lies exactly on the margin boundary as before. However, when $\xi_n > 0$, the support vector may lie elsewhere, possibly far from the margin. To finish up, let me introduce two simple but important technical observations. 

First, if the data is not linearly separable, the hard margin method doesn’t work well, and the connection between the primal and dual forms might breaks down. Second, if there is an extra weight term like $w_0$, known as threshold, it can be combined into the bias $b$, and $w_0$ becomes zero. So, we don't have to worry. 

These points show why we sometimes need to go beyond the basic hard margin approach.



