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

##### 3.2. polynominal model without regularizaiton. 

The case of polynomial regression with the squared-error measure illustrates the main ideas of regularization effectively and provides a solid mathematical foundation. Although we focus on this case for clarity, the concepts we discuss extend naturally to non-linear and multi-dimensional settings with more general error measures.

Polynomial models, in fact, are a special case of linear models in a transformed space $\mathcal{Z}$, defined by a nonlinear mapping $\Phi : \mathcal{X} \rightarrow \mathcal{Z}$. In the case of a $Q$th-order polynomial model, $\Phi$ transforms the input $x$ into a vector $\mathbf{z}$ of Legendre polynomials: 

<br>

$$
\mathbf{z} =
\begin{bmatrix}
1 \\
L_1(x) \\
\vdots \\
L_Q(x)
\end{bmatrix}
$$

<br>

Our hypothesis set $\mathcal{H}_Q$ is a linear combination of these polynomials:

<br>

$$
\mathcal{H}_Q = \left\{ h \;\middle|\; h(x) = \mathbf{w}^\top \mathbf{z} = \sum_{q=0}^{Q} w_q L_q(x) \right\}
$$

<br>

where $L_0(x) = 1$. As usual, we will sometimes refer to the hypothesis $h$ by its weight vector $\mathbf{w}$. Since each $h$ is linear in $\mathbf{w}$, we can use the machinery of linear regression from [Lecture 3](https://isopink.github.io/Linear-Model-L/) to minimize the squared error:

<br>

$$
E_{\text{in}}(\mathbf{w}) = \frac{1}{N} \sum_{n=1}^{N} (\mathbf{w}^\top \mathbf{z}_n - y_n)^2
$$

<br>

We can write it down with matrix notation as: 

<br>

$$
E_{\text{in}}(\mathbf{w}) = \frac{1}{N} \left\| \mathbf{Zw} - \mathbf{y} \right\|^2
$$

<br>

By using the pseudo-inverse, the optimal weights that mininize the $E_{\text{in}}$ can be computed as: 

<br>

$$
\mathbf{w}_{\text{lin}} = (\mathbf{Z}^\top \mathbf{Z})^{-1} \mathbf{Z}^\top \mathbf{y}
$$

<br>

This solution is computed without any constraint. What if we constrain the weights? 

<br>

##### 3.2. polynominal model with regularizaiton

We have already seen an example of constraining the weights in [Lecture 11](https://isopink.github.io/Overfitting/).
The set of 2nd-order polynomials can be thought of as a constrained version of the set of 10th-order polynomials in the sense that some of the 10th-order polynominal's weights are required to be zero. In conclusion, we can establish the relationship between two hypothesis sets as below:

<br>

$$
\mathcal{H}_2 = \{ \mathbf{w} \mid \mathbf{w} \in \mathcal{H}_{10};\ w_q = 0\ \text{for}\ q \geq 3 \}
$$

<br>

Requiring some weights to be 0 is a *hard* constraint. Instead of requiring some weights to be zero, we can force the weights to be small but not necessarily zero through a softer constraint such as

<br>

$$
\sum_{q=0}^{Q} w_q^2 \leq C
$$

<br>

With this inspection, optimization of $E_{\text{in}}$ problem becomes: 

<br>

$$
\min_{\mathbf{w}} E_{\text{in}}(\mathbf{w}) \quad \text{subject to} \quad \mathbf{w}^\top \mathbf{w} \leq C
$$

<br>

We define $\mathbf{w}_{\text{reg}}$ to diffrentiate this solution with the unconstrained solution. Now let us examine how to solve the constrained situation. I could have explained it through mathematical way, I will include figures and intuitive explanations to aid the readers' understanding.

![solution](/assets/images/rr_5.svg) 

The unconstrained $E_{\text{in}}$ forms a blue ellipse centered at $\mathbf{w}_{\text{lin}}$, while the constraint is shown as a red circle. The optimal solution lies where the two regions overlap.

To minimize $E_{\text{in}}$, consider a point $\mathbf{w}$ in the overlap region. The gradient of $E_{\text{in}}$ points outward from the blue ellipse, and the normal vector of the red circle does the same. Thus, to reduce $E_{\text{in}}$, $\mathbf{w}$ should move along the red boundary toward $\mathbf{w}_{\text{lin}}$.

If $\mathbf{w}_{\text{reg}}$ is to be optimal while remaining on the boundary, then for some positive parameter $\lambda$,

<br>

$$
\nabla E_{\text{in}}(\mathbf{w}_{\text{reg}}) = -2 \lambda \mathbf{w}_{\text{reg}}
$$

<br>

Equivalently, $\mathbf{w}_{\text{reg}}$ satisfies: 

<br>

$$
\nabla \left( E_{\text{in}}(\mathbf{w}) + \lambda \mathbf{w}^\top \mathbf{w} \right) \Big|_{\mathbf{w} = \mathbf{w}_{\text{reg}}} = \mathbf{0}
$$

<br>

So, for some $\lambda > 0$, $\mathbf{w}_{\text{reg}}$ locally minimizes:

<br>

$$
E_{\text{in}}(\mathbf{w}) + \lambda \mathbf{w}^\top \mathbf{w}
$$

<br>

The constant $C$ disappears in the expression and is replaced by $\lambda$. Fortunately, as $C$ increases, $\lambda$ decreases, and vice versa. So, adjusting $\lambda$ has the same effect as controlling $C$. We call this form as Augmented error:

<br>

$$
E_{\text{aug}}(\mathbf{w}) = E_{\text{in}}(\mathbf{w}) + \lambda \mathbf{w}^\top \mathbf{w}
$$

<br>

When $\lambda = 0$, we recover the usual $E_{\text{in}}$. For $\lambda > 0$, the penalty term $\mathbf{w}^\top \mathbf{w}$ introduces a tradeoff between fitting the data and keeping the weights small. This effectively limits the hypothesis set, leading to better generalization. Now, we will introduce how to find constrained solution. By modifying $\lambda$, $E_{\text{aug}}$ can be described as below: 

<br>

$$
E_{\text{aug}}(\mathbf{w}) = E_{\text{in}}(\mathbf{w}) + \frac{\lambda}{N} \mathbf{w}^\top \mathbf{w}
$$

<br>

We have calculated $E_{\text{in}}$ at (3.2). So, our equation becomes: 

<br>

$$
\frac{1}{N} \left( (\mathbf{Z}\mathbf{w} - \mathbf{y})^\top (\mathbf{Z}\mathbf{w} - \mathbf{y}) + \lambda\, \mathbf{w}^\top \mathbf{w} \right)
$$

<br>

Then, defferntiate with respect to $\mathbf{w}$:

<br>

$$
\nabla E_{\text{aug}}(\mathbf{w}) = \mathbf{0} \quad \Longrightarrow \quad \mathbf{Z}^\top (\mathbf{Z}\mathbf{w} - \mathbf{y}) + \lambda \mathbf{w} = \mathbf{0}
$$

<br>

Now we can compute the $\mathbf{w}_{\text{reg}}$ as below: 

<br>

$$
\mathbf{w}_{\text{reg}} = \left( \mathbf{Z}^\top \mathbf{Z} + \lambda \mathbf{I} \right)^{-1} \mathbf{Z}^\top \mathbf{y}
$$

<br>

We can now apply $\mathbf{w}_{\text{reg}}$ to the overfitting example. Let us recall the previous example we discussed at [lecture 11](https://isopink.github.io/Overfitting/). The results for different $\lambda$'s are shown below: 

![solution](/assets/images/rr_6.svg) 

As you can see, even very little regularization goes a long way, but too much regularization results in an overly flat curve at the expense of in-sample fit.  

---

#### 4. Weight decay

The method described in (3.2) is called Weight Decay. To understand why it is called that, let us consider the case of using gradient descent. We have seen how gradient descent works in [Lecture 9](https://isopink.github.io/Linear-Model-ll/). It can be described as below, using unconstrained error function: 

<br>

$$
\mathbf{w}(t + 1) = \mathbf{w}(t) - \eta \nabla e_n(\mathbf{w})
$$

<br>

However, if we use constrained error function, the equation becomes as below : 

<br>

$$
\begin{aligned}
\mathbf{w}(t + 1) 
&= \mathbf{w}(t) - \eta \nabla E_{\text{in}}(\mathbf{w}(t)) - 2\eta \mathbf{w}(t) \\ \\
&= \mathbf{w}(t) \left(1 - 2\eta \lambda \right) - \eta \nabla E_{\text{in}}(\mathbf{w}(t))
\end{aligned}
$$

<br>

Each time $t$ increases, $\mathbf{w}(t)$ becomes slightly smaller. This gradual shrinkage is the reason the method is called Weight Decay.

<br>

---

#### 5. Choosing a regularzier 



