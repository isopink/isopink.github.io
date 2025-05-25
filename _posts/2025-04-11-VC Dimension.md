---
layout: single
title: "Lecture 7 : VC dimension"
---
 
In this time, we now introduce the **VC dimension**. At the end of the last session, we introduced *VC bound*. We will dive into that topic. The discussion will proceed in following four parts: 

1. The definition of VC diemnsion

2. VC dimension of perceptrons

3. Interpreting the VC dimension

4. Generalization bounds

---

#### 1. The definition of VC dimension

If you rememeber the defition of *break point*, which we learnd in [Lecture 5](https://isopink.github.io/Effective-number-of-hypothesis/), you can easily accept the difinition of VC dimension. 

The Vapnik–Chervonenkis dimension of a hypothesis set $\mathcal{H}$, denoted by $d_{\text{VC}}(\mathcal{H})$ or simply $d_{\text{VC}}$, is the largest value of $N$ for which $ m_{\mathcal{H}}(N) = 2^N.$ 

If $d_{\text{VC}}$ is the VC dimension of $\mathcal{H}$, then **$k = d_{\text{VC}} + 1$** is a break point for $m_{\mathcal{H}}$, since $m_{\mathcal{H}}(N)$ cannot equal $2^N$ for any $N > d_{\text{VC}}$ by definition. Since $k = d_{\text{VC}} +1$, our previous Growth funtion with polynominal bound can be rewritten as : 

<br>

$$
m_{\mathcal{H}}(N) \leq \sum_{i=0}^{k-1} \binom{N}{i} = \sum_{i=0}^{d_\text{VC}} \binom{N}{i}
$$

<br>

Maximum power of growth function is now $N^{d_\text{VC}}$. the VC dimension is the order of the polynominal bound on $m_\mathcal{H}(N)$. This can be lead to the following statement: 

<br>

$$
d_{\text{VC}}(\mathcal{H}) \text{ is finite} \quad \Rightarrow \quad g \in \mathcal{H} \text{ will generalize}
$$

<br>

---

#### 2. VC dimension of perceptrons 

In general, the VC dimension of a $d$-dimensional perceptron is $d+1$. This is consistent with our previous perceptron [exmaple](https://isopink.github.io/Effective-number-of-hypothesis/), where the $2D$ perceptron has the break point $4$. To prove the VC dimension of $d$-dimiensional perceptron, We will show two statements, $d_{\text{VC}} \leq d + 1$ and $d_{\text{VC}} \geq d + 1$

<br>

##### 2.1. $d_{\text{VC}} \geq d + 1$

To show that $d_{\text{VC}} \geq d + 1$, Let us find $d+1$ points in $d$-dimensional input space $\mathcal{X}$ can be shattered by perceptron. We prepare $d+1$ points in $d$-dimensional space. Since the $0th$ coordinate is for the threshold, forming a matrix $X$ using their transposes yields a square matrix. If the points are linearly independent, $X$ is invertible. It is described as: 

<br>

$$
\mathbf{X} =
\begin{bmatrix}
\mathbf{x}_1^\top \\
\mathbf{x}_2^\top \\
\mathbf{x}_3^\top \\
\vdots \\
\mathbf{x}_{d+1}^\top
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & 0 & \cdots & 0 \\
1 & 1 & 0 & \cdots & 0 \\
1 & 0 & 1 & \cdots & 0 \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
1 & 0 & 0 & \cdots & 1
\end{bmatrix}
$$

<br>

Now, we randomly assign values to the output vector $y$ in the dataset:

<br>

$$
\mathbf{y} =
\begin{bmatrix}
y_1 \\
y_2 \\
\vdots \\
y_{d+1}
\end{bmatrix}
=
\begin{bmatrix}
\pm 1 \\
\pm 1 \\
\vdots \\
\pm 1
\end{bmatrix}
$$

<br>

Can we find a vector $w$ satisfying $\text{sign}(Xw) = y$? It is easy. Just make $Xw =y$. By nonsingularity of $X$: 

<br>

$$
\mathbf{w} = \mathbf{X}^{-1} \mathbf{y}
$$

<br>

We can shatter these $d+1$ points. This implies $d_{\text{VC}} \geq d + 1$. 

<br>

##### 2.2. $d_{\text{VC}} \leq d + 1$

To show that $d_{\text{VC}} \leq d + 1$, we need to show no set of $d+2$ points in $d$-dimensional input space $\mathcal{X}$ can be shattered by the perceptron. Let's consider creating $d+2$ arbitrary points in a $d$-dimensional space. Since the number of points exceeds the number of dimensions, it is impossible for all the points to be linearly independent. We must have nonzero $a_i$ where : 

<br>

$$
\mathbf{x}_j = \sum_{i \ne j} a_i \, \mathbf{x}_i
$$

<br>

Now, consider the following dichotomy. Let $x_i$'s with nonzero $a_i$ get $y_i = \text{sign}(a_i)$, and $x_j$ gets $y_j = -1$. Can any perceptron implement such dichotomy? The answer is "NO". Let me tell you why. Consider following statement. 

<br>

$$
\mathbf{x}_j = \sum_{i \ne j} a_i \, \mathbf{x}_i 
\quad \Rightarrow \quad 
\mathbf{w}^\top \mathbf{x}_j = \sum_{i \ne j} a_i \, \mathbf{w}^\top \mathbf{x}_i
$$

<br>

If $y_i = \text{sign}(\mathbf{w}^\top \mathbf{x}_i) = \text{sign}(a_i), \text{ then } a_i \, \mathbf{w}^\top \mathbf{x}_i > 0$. Therefore, $y_j = \text{sign}(\mathbf{w}^\top \mathbf{x}_j) = +1$. 

<br>

##### 2.3. Putting it together 

We proved $d_{\text{VC}} \geq d + 1$ and $d_{\text{VC}} \leq d + 1$. That is to say: 

<br>

$$
d_{\text{VC}} = d + 1
$$

<br>

The perceptron case provides a nice intuition about the VC dimension, since $d + 1$ is also the number of parameters in the model. However, there are more interpretation of VC dimension. We now introduce that. 

---

#### 3. Interpreting the VC dimension

We will explore two interpretations of the VC dimension. One is **degrees of freedom**, and the other is **Amount of data required**.

<br>

##### 3.1. Degree of freedom  

The VC dimension measures effective parameters or degrees of freedom that enable the model to express a diverse set of hypotheses. In the case of perceptrons, the effective parameters correspond to explicit parameters in the model, namely $w_0, w_1, \cdots, w_d$. In other models, the effective parameters may be less obviuos or implicit. Let's see some examples. 

![solution](/assets/images/vc_1.svg) 

In the Positive Ray example, whether the data is labeled $+1$ or $-1$ is determined by the position of parameter $a$. In other words, this example has 1 parameter, VC dimension of 1, and 1 degree of freedom.

Similarly, in the Positive Interval example, two points are needed to define the interval. Thus, there are 2 parameters, and both the VC dimension and degrees of freedom are also $2$.

![solution](/assets/images/vc_2.svg) 

Let’s look at an example where we stack four 1-dimensional perceptrons in a row. Each perceptron only takes one input and uses two parameters, $w_0$ and $w_1$. So in total, we have $8$ parameters.

At first, it might seem like there are 8 degrees of freedom, since we have 8 parameters. But if you look more carefully, every perceptrons can only make output $+1$ or $-1$. That means the input to the next perceptron is also just $+1$ or $-1$. Because of this, even though there are $8$ parameters, the actual degrees of freedom is only $2$.

We can also use the VC dimension to figure this out more easily. If each perceptron is $1$-dimensional, the VC dimension is 2, which matches our earlier result. That means the number of degrees of freedom is also 2.

<br>

##### 3.2. Amount of data required

The second interpretation of VC dimension is, It provides a proper number of data to qualifiy the VC Inequality. Let's look at the following statement: 

<br>

$$
\mathbb{P}\left[ \left| E_{\text{in}}(g) - E_{\text{out}}(g) \right| > \epsilon \right] 
\leq 
\underbrace{4 m_{\mathcal{H}}(2N) e^{- \frac{1}{8} \epsilon^2 N}}_{\delta}
$$

<br>

If we want certain $\epsilon$ and $\delta$, how does $N$ depend on $d_\text{VC}$? This is our question. Let's first simplify the right-hand side, which is currently in a rather complex form. If we keep only the $N$-dependent part of the exponential term and discard the rest of the complicated expression,  
we can represent it as:

$$
N^d e^{-N} \quad \text{Where} \quad d = d_\text{VC}
$$

We want this value to be less than $1$. How deos $N$ chage with $d$?. Here is the plot: 

![solution](/assets/images/vc_3.svg) 

Instead of calculating exact value $N$, here is the **Rule of thumb**: 

<br>

$$
N \geq 10 d_{\text{VC}}
$$

<br>

Suppose that we have a learning model with $d_{\text{VC}} = 3$ and would like the generalization error to be at most $0.1$ with confidence $0.9$  
(so $\epsilon = 0.1$ and $\delta = 0.1$). How big a data set do we need? We could calculate this using rigorous mathematics, but by **Rule of thumb** instead, We can estimate that $N \approx 30{,}000$.  

---

#### 4. Generalization bounds 

Let's use the **VC dimension** to roughly estimate the **upper and lower bounds** of the variables used in the **VC Inequality** : 

<br>

$$
\mathbb{P}\left[ \left| E_{\text{in}}(g) - E_{\text{out}}(g) \right| > \epsilon \right] 
\leq 
\underbrace{4 m_{\mathcal{H}}(2N) e^{- \frac{1}{8} \epsilon^2 N}}_{\delta}
$$

<br>

Get $\epsilon$ in terms of $\delta$ : 

<br>

$$
\delta = 4 m_{\mathcal{H}}(2N) \, e^{- \frac{1}{8} \epsilon^2 N} 
\quad \Rightarrow \quad 
\epsilon = \sqrt{ \frac{8}{N} \ln \left( \frac{4 m_{\mathcal{H}}(2N)}{\delta} \right) }
$$

<br>

If we define the right-hand side of $\epsilon$ as a function $\Omega$, then this function $\Omega$ can be expressed as depending on the **number of data points** $N$, the **hypothesis set** $\mathcal{H}$, and the $\delta$ of the VC inequality. Now, we can simply put this : 

<br>

$$
\text{With probability } \geq 1 - \delta,\quad 
\left| E_{\text{out}} - E_{\text{in}} \right| \leq \Omega
$$

<br>

Which means, There exist the **Good Event** at least the probability with $1-\delta$. Rearranging is now complete. In general, $E_{\text{out}}$ is bigger than $E_{\text{in}}$. Because $E_{\text{in}}$ is the term we minimize deliberately. With this inspection, **Generalization bound** is :

<br>

$$
\text{With probability } \geq 1 - \delta,\quad E_{\text{out}} \leq E_{\text{in}} + \Omega
$$

<br>

If we use the polynomial bound based on $d_{VC}$ instead of $m_{\mathcal{H}}(2N)$, we get another valid bound on the out-of-sample error : 

<br>

$$
E_{\text{out}}(g) \leq E_{\text{in}}(g) + \sqrt{\frac{8}{N} \ln\left(\frac{4((2N)^{d_{VC}} + 1)}{\delta}\right)}
$$

<br>

When we use a more complex learning model, one that has higher VC dimension $$d_{VC}$$, we are likely to fit the training data better resulting in a lower $E_\text{in}$, but we pay a higher penalty for model complexity. The upper bound of $E_\text{out}$ goes up. A combination of the two attains a minimum at some intermediate $$d_{VC}^*$$. There is tradeoff between Approximation and Generlization.   

![solution](/assets/images/vc_4.svg) 


