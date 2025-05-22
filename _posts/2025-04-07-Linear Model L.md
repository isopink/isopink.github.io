---
layout: single
title: "Lecture 3 : The Linear Model I"
---

In this time, I am going to introduce some Linear Model. This part is not directly related to the previous or next chapters.
Nevertheless, it will be used for deeper concepts later. The discussion will proceed in the following four parts :   

1. Input representation

2. Linear Classification    

3. Linear Regression     

4. Nonlinear Transformation    

---

#### 1. Input representation 

![solution](/assets/images/lin_1.svg) 

Let’s begin with an example of classifying handwritten digits. Each image is made up of 16 by 16 pixels. First, we need to convert the image into numerical data. If we treat this as $256 + 1$ inputs and a corresponding weight vector, the input and weight vector would look like this: 

<br>

$$
\mathbf{X} = (x_0, x_1, x_2, \cdots, x_{256})
$$

<br>

<br>

$$
\mathbf{W} = (w_0, w_1, w_2, \cdots, w_{256})
$$

<br>

Intuitively, you can tell that this will involve a lot of computation. We should extract useful information, such as intensity and symmetry. Simply put, intensity is the number of black pixels, and symmetry is whether the input data is symmetric. Then, the input and weight model can be simplified as follows:

<br>

$$
\mathbf{X} = (x_0, x_1, x_2) \quad \mathbf{W} = (w_0, w_1, w_2) 
$$

<br>

*Optional*: We define asymmetry as the average absolute difference between an image and its flipped versions, and symmetry as the negation of asymmetry. Digit 1 would result in a higher symmetry value. 

---

#### 2. Linear Classification

With this representation, we can expect significantly fewer computations. Let’s now classify the digits. Before classifying all digits, we start by separating them two at a time. This “multiclass to binary classification” approach is commonly used in many learning algorithms. We first classify $1$ and $5%. Digit $5$ has more black pixels than digit $1$, and while $1$ is symmetrical, $5$ is not — so it shouldn’t be too difficult to distinguish between the two. 

![solution](/assets/images/lin_2.svg) 

We thought that the data could be well separated, but some points appear hard to classify — even visually. This dataset does not seem linearly separable. As a result, the Perceptron Learning Algorithm (PLA) remain unstable. 

![solution](/assets/images/lin_3.svg) 

So we stop the algorithm manually at iteration 1000. The PLA applied here results in a final boundary as shown. It seems that $E_{\text{out}}$ tracks $E_{\text{in}}$. However, the boundary found after 1000 iterations doesn’t appear to be optimal. If you look at the left plot, you’ll notice that the Ein at iteration 1000 is not the minimum. So we need a better boundary. I think this is the right time to introduce you to the Pocket Algorithm. 

![solution](/assets/images/lin_4.svg) 

This algorithm keeps the best-performing weight vector encountered during the iterations. As you can see from the right plot, after around 100 iterations, there are no further changes — this is the best-performing weight vector. The algorithm works as follows: 

<br>

> **The pocket algorithm:**
> 1. Set the pocket weight vector $\hat{\mathbf{w}}$ to $\mathbf{w}(0)$ of PLA.  
> 2. for $t = 0, \dots, T - 1$ do  
> 3. &nbsp;&nbsp;&nbsp;&nbsp;Run PLA for one update to obtain $\mathbf{w}(t + 1)$.  
> 4. &nbsp;&nbsp;&nbsp;&nbsp;Evaluate $E_{\text{in}}(\mathbf{w}(t + 1))$.  
> 5. &nbsp;&nbsp;&nbsp;&nbsp;If $\mathbf{w}(t + 1)$ is better than $\hat{\mathbf{w}}$ in terms of $E_{\text{in}}$, set $\hat{\mathbf{w}}$ to $\mathbf{w}(t + 1)$.  
> 6. Return $\hat{\mathbf{w}}$.

<br>

We can now visualize the difference between the original boundary and the updated one: 

![solution](/assets/images/lin_5.svg)

Although the data is not linearly separable, the boundary found by the pocket algorithm is clearly more desirable. 

---

#### 3. Linear Regression

So far, we’ve covered classification problems with discrete outputs. Now let’s deal with regression, where the output is a real-value. Let’s revisit the [__credit approval example__](https://isopink.github.io/Learning-problem/). This time, we want to determine a credit line. Here's the input table.

<br>

| Feature             | Value      |
|---------------------|------------|
| age                 | 23 years   |
| annual salary       | $30,000    |
| years in residence  | 1 year     |
| years in job        | 1 year     |
| current debt        | $15,000    |
| ⋯                   | ⋯          |

<br>

This time we need *real-values* (not binary!), so the output of our linear regression will look like the classification model without the sign — that is, $h(x) = w^T x$. Now here's the new question: **How well does $h(x) = w^T x$ approximate $f(x)$?** 


Since the problem is different, we also need a different way to measure error. In classification, we only cared about whether the output was $+1$ or $-1$, so we could just count how many were wrong and report a ratio. But in regression, outputs can take infinitely many values — so it’s not enough to just ask whether it was right or wrong. For example, if the true value is 1000, then predicting 950 and predicting 5000 are both wrong — but not equally wrong. So **we need to measure how big the difference was**.


There are many ways to do this, but in this lecture we’ll use the **squared error** — the square of the difference between the hypothesis and the target. The *in-sample error* is defined as: 

<br>

$$
E_{\text{in}}(h) = \frac{1}{N} \sum_{n=1}^{N} \left( h(\mathbf{x}_n) - y_n \right)^2
$$

<br>

To minimize this error, we’ll use the **Least Squares Method** from linear algebra. First, let’s rewrite the *in-sample error* using matrix and vector notation: 

<br>

$$
E_{\text{in}}(\mathbf{w}) 
= \frac{1}{N} \left\| \mathbf{X} \mathbf{w} - \mathbf{y} \right\|^2
$$

<br>

$$
\text{Where,} \quad
\mathbf{X} =
\begin{bmatrix}
\mathbf{x}_1^\top \\
\mathbf{x}_2^\top \\
\vdots \\
\mathbf{x}_N^\top
\end{bmatrix}
,\quad
\mathbf{y} =
\begin{bmatrix}
y_1 \\
y_2 \\
\vdots \\
y_N
\end{bmatrix}
$$

<br>

Minimizing this error is equivalent to solving the linear equation $Xw = y$ using a least-squares solution.
To do that, we solve the normal equation:

<br>

$$X^T X w = X^T y$$

<br>

If $X$ has linearly independent columns, we can multiply both sides by the inverse of $X^T X$ and find the optimal weight vector: 

<br>

$$
\hat{w} = \left( \mathbf{X}^\top \mathbf{X} \right)^{-1} \mathbf{X}^\top y
$$

<br>

$\left( \mathbf{X}^\top \mathbf{X} \right)^{-1} \mathbf{X}^\top$ is called the *pseudo-inverse*, $X^\dagger$ 

<br>

**Remark**: If $X^T X$ is not invertible, we can still define a *pseudo-inverse*, but the solution won’t be unique. Fortunately, in practice, $X$ typically has independent columns. To handle non-invertibility, we would need to discuss *SVD* — but that’s too much for now. You can check one of my other posts for that.


Here’s an extra insight: Linear regression gives real-valued outputs. But classification outputs $+1$ or $-1$ — those are real numbers too, so maybe there’s a connection. Of course, regression and classification have different objectives, so we can’t directly reuse the model. However, we can use the regression-trained weights to speed up convergence during classification. Instead of initializing $w$ randomly (or with a zero vector), starting with the regression result can save a lot of time. 

![solution](/assets/images/lin_6.svg)

---

#### 4. Nonlinear Transformation 

So far, we’ve talked about linear models. But linear in what? This is the important question. All the formulas we used were linear not only in $x$, but also in $w$. Upon closer inspection of the learning algorithm, we find that **linearity in $w$ is the key feature**. This means we can use nonlinear features of $x$ while still keeping things linear in $w$. 

![solution](/assets/images/lin_7.svg) 

Clearly, a linear classifier won’t work on this dataset. However, if we transform $x_1$, $x_2$ into $x_1^2$, $x_2^2$, we may be able to separate the data. A circle corresponds to the equation: 

<br>

$$
x_1^2 + x_2^2 = 0.6
$$

<br>

That is, the nonlinear hypothesis $h(x) = \text{sign}(-0.6 + x_1^2 + x_2^2)$ separates the dataset perfectly. We can now view this hypothesis as a linear model after applying a nonlinear transformation to $x$. We now introduce the **Z-space** — a space containing the transformed vector $z$. Let $z_0 = 1$, $z_1 = x_1^2$ and $z_2 = x_2^2$. The formula can be written as: 

<br>

$$
h(\mathbf{x}) =
\text{sign} \left(
\underbrace{(-0.6)}_{\tilde{w}_0} \cdot \underbrace{1}_{z_0}
+ \underbrace{1}_{\tilde{w}_1} \cdot \underbrace{x_1^2}_{z_1}
+ \underbrace{1}_{\tilde{w}_2} \cdot \underbrace{x_2^2}_{z_2}
\right)
$$

<br>

<br>

$$
= \text{sign} \left(
\underbrace{[\tilde{w}_0 \quad \tilde{w}_1 \quad \tilde{w}_2]}_{\tilde{\mathbf{w}}^\top}
\underbrace{
\begin{bmatrix}
1 \\
z_1 \\
z_2
\end{bmatrix}
}_{\mathbf{z}}
\right)
$$

<br>

So, $z$ is obtained by applying a nonlinear transformation $\Phi$ to $x$. This transformation $\Phi$ is called a feature transform. In our case, $\Phi$ is: 

<br>

$$
\Phi(\mathbf{x}) = (1, x_1^2, x_2^2).
$$

<br>

And here is summary of **What transforms to waht?** :

![solution](/assets/images/lin_8.svg)

The goal is to find the weights — so this is the key. However, since we don’t compute the weights directly in the $X$ space, there is no weight vector in the $X$ space. The weights are computed in the $Z$ space, so only $\tilde{w}$ exists. That said, we are given $x$ as input, and we must perform classification or regression using $g(x)$. Therefore, the hypothesis $g(x)$ is defined as:

<br>

$$
g(\mathbf{x}) = \text{sign}(\tilde{\mathbf{w}}^\top \Phi(\mathbf{x}))
$$

<br>

However, there’s one more important thing: some points in the $z \in Z$ space may not be valid transforms of any $x \in X$. Also, multiple $x \in X$ values may transform into the same $z \in Z$. In other words, we may not be able to invert $\Phi$. This is why we don’t define $\hat{w}$ in the $X$ space as $\Phi^{-1}(\hat{w})$. 

