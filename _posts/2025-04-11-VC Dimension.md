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

If you rememeber the defition of *break point*, which we learnd in [<u>Lecture 5</u>](https://isopink.github.io/Effective-number-of-hypothesis/), you can easily accept the difinition of VC dimension. 

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

In general, the VC dimension of a $d$-dimensional perceptron is $d+1$. This is consistent with our previous perceptron [<u>exmaple</u>](https://isopink.github.io/Effective-number-of-hypothesis/), where the $2D$ perceptron has the break point $4$. To prove the VC dimension of $d$-dimiensional perceptron, We will show two statements, $d_{\text{VC}} \leq d + 1$ and $d_{\text{VC}} \geq d + 1$

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

The VC dimension measures these effective parameters or **degrees of freedom** that enable the model to express a diverse set of hypotheses. In the case of perceptrons, the effective parameters correspond to explicit parameters in the model, namely $w_0, w_1, \cdots, w_d$. In other models, the effective parameters may be less obviuos or implicit. Let's see some examples. 

![solution](/assets/images/vc_1.svg) 

In the *Positive Ray* example, whether the data is labeled $+1$ or $-1$ is determined by the position of parameter $a$. In other words, this example has **1 parameter**, **VC dimension of 1**, and **1 degree of freedom**.

Similarly, in the *Positive Interval* example, two points are needed to define the interval. Thus, there are **2 parameters**, and both the **VC dimension** and **degrees of freedom** are also $2$.

![solution](/assets/images/vc_2.svg) 

Let's take a look at an example where **four 1-dimensional perceptrons** are stacked sequentially. Since each perceptron is $1$-dimensional, each one uses **two parameters**, $w_0$ and $w_1$. This means the total number of parameters is $2 + 2 + 2 + 2 = 8$.

At first glance, it may seem that there are **8 degrees of freedom** because there are 8 parameters. However, if you look more closely, the output of the **first perceptron** can only be either $+1$ or $-1$. This means that the input to the **second perceptron** can also only be one of two values: $+1$ or $-1$. The same applies to the **third** and **fourth perceptrons**. Therefore, the actual number of degrees of freedom in this example is **2**.

If we use the **VC dimension** to determine the degrees of freedom, the process becomes much simpler than counting parameters. Since each perceptron is $1$-dimensional, $d = 1$. The VC dimension of a perceptron is $d + 1$, so in this case, $d_{\text{VC}} = 2$. Since the **VC dimension equals the degrees of freedom**, we can immediately conclude that the number of degrees of freedom is **also 2**. 

<br>

##### 3.2. Amount of data required

