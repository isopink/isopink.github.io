---
layout: single
title: "Lectrue 6 : Theory of Generlization"
---

In this time, we will discuss the mathematical proof of [$m_{\mathcal{H}}(N)$](https://isopink.github.io/Effective-number-of-hypothesis/). This is the most difficult part of this course. You need to pay attention! The discussion will proceed in the following two parts :

1. Proof that $m_{\mathcal{H}}(N)$ is polynominal

2. proof that $m_{\mathcal{H}}(N)$ can replace $m$ 


---

#### 1. Proof that $m_{\mathcal{H}}(N)$ is polynominal

Let $B(N,K)$ is the maximum number of dichotomies of $N$ points such that no subset of size $k$ of the $N$ points can be shattered by these dichotomies. Since $B(N,K)$ is defined as a maximum, it will serve as an upper bound for any $m_\mathcal{H}(N)$ that has a break point $k$: 

<br>

$$
m_{\mathcal{H}}(N) \leq B(N, k)
$$

<br>

If we show $B(N,K) \leq \text{Polynominal}$, the game is over. Let us begin. I listed dichotomies of $B(N,K)$ in the follownig table: 

<br>

$$
\begin{array}{c|c|c c c c|c}
& \# \text{ of rows} & \mathbf{x}_1 & \mathbf{x}_2 & \cdots & \mathbf{x}_{N-1} & \mathbf{x}_N \\
\hline
&                 & +1 & +1 & \cdots & +1 & +1 \\
&                 & -1 & +1 & \cdots & +1 & -1 \\
S_1 & \alpha      & \vdots & \vdots & \ddots & \vdots & \vdots \\
&                 & +1 & -1 & \cdots & -1 & -1 \\
&                 & -1 & +1 & \cdots & -1 & +1 \\
\hline
&                 & +1 & -1 & \cdots & +1 & +1 \\
&                 & -1 & -1 & \cdots & +1 & +1 \\
S_2^+ & \beta     & \vdots & \vdots & \ddots & \vdots & \vdots \\
&                 & +1 & -1 & \cdots & -1 & +1 \\
&                 & -1 & -1 & \cdots & -1 & +1 \\
\hline
&                 & +1 & -1 & \cdots & +1 & -1 \\
&                 & -1 & -1 & \cdots & +1 & -1 \\
S_2^- & \beta     & \vdots & \vdots & \ddots & \vdots & \vdots \\
&                 & +1 & -1 & \cdots & -1 & -1 \\
&                 & -1 & -1 & \cdots & -1 & -1 \\
\end{array}
$$


<br>

Consider the dichotomies except the $\mathbf{x}_N$ column. Some dichotomies on these $N - 1$ points appear only once (with either $+1$ or $-1$ in the $\mathbf{x}_N$ column, but not both). We collect these dichotomies in the set $S_1$.

The remaining dichotomies on the first $N - 1$ points appear twice, once with $+1$ and once with $-1$ in the $\mathbf{x}_N$ column. We collect these dichotomies in the set $S_2$ which can be divided into two equal parts, $S_2^+$ and $S_2^-$ (with $+1$ and $-1$ in the $\mathbf{x}_N$ column, respectively). 

Let $S_1$ have $\alpha$ rows, and let $S_2^+$ and $S_2^-$ have $\beta$ rows each. Since the total number of rows in the table is $B(N, k)$ by construction, we have: 

<br>

$$
B(N, k) = \alpha + 2\beta.
$$

<br>

The total number of different dichotomies on the first $N - 1$ points is given by $\alpha + \beta$; since $S_2^+$ and $S_2^-$ are identical on these $N - 1$ points, their dichotomies are redundant. Since no subset of $k$ of these first $N - 1$ points can be shattered (since no $k$-subset of all $N$ points can be shattered), we deduce that :

<br>

$$
\alpha + \beta \leq B(N - 1, k)
$$

<br>

Further, no subset of size $k - 1$ of the first $N - 1$ points can be shattered by the dichotomies in $S_2^+$. If there existed such a subset, then taking the corresponding set of dichotomies in $S_2^-$ and adding $\mathbf{x}_N$ to the data points yields a subset of size $k$ that is shattered, which we know cannot exist in this table by definition of $B(N, k)$. Therefore,

<br>

$$
\beta \leq B(N-1, K-1)
$$

<br>

Substituting the two Inequalities, we get: 

<br>

$$
B(N, K) \leq B(N-1, K) + B(N-1, K-1) 
$$

<br>

We can use it recursively to compute a bound on $B(N, K)$, as shwon in the following table: 

<br>

$$
\begin{array}{c c|cccccc}
    &   &  &   &k   &   &   &   \\ 
    &   & 1 & 2 &   & 3 & 4 & 5 \\
\hline
  & 1 & 1 & 2 &   & 2 & 2 & 2 \\
  & 2 & 1 & 3 &   & 4 & 4 & 4 \\
N &   &   &   &\searrow   & \downarrow &   &   \\ 
  & 3 & 1 & 4 &   & 7 & 8 & 8 \\
  & 4 & 1 & 5 &   &11 & \cdots & \cdots \\
  & 5 & 1 & 6 &   &\cdots & \cdots &   \\
  & 6 & 1 & 7 &   &\cdots &        &   \\
\end{array}
$$

<br>

To continue the proof, let me introduce Sauer's lemma: 

<br>

$$
B(N, k) \leq \sum_{i=0}^{k-1} \binom{N}{i}
$$

<br>

*Proof*. The statement is true whenever $k = 1$ or $N = 1$, by inspection. The proof is by induction on $N$. Assume the statement is true for all $N \leq N_o$ and all $k$. We need to prove the statement for $N = N_o + 1$ and all $k$. Since the statement is already true when $k = 1$ (for all values of $N$) by the initial condition, we only need to worry about $k \geq 2$. We are going to apply induction hypotehsis to each term on the right-hand-side of following Inequality: 

<br>

$$
B(N_o + 1, k) \leq B(N_o, k) + B(N_o, k - 1)
$$

<br>

By applying induction, we get: 

<br>

$$
\begin{aligned}
B(N_o + 1, k) &\leq \sum_{i=0}^{k-1} \binom{N_o}{i} + \sum_{i=0}^{k-2} \binom{N_o}{i} \\
&= 1 + \sum_{i=1}^{k-1} \binom{N_o}{i} + \sum_{i=1}^{k-1} \binom{N_o}{i - 1} \\
&= 1 + \sum_{i=1}^{k-1} \left[ \binom{N_o}{i} + \binom{N_o}{i - 1} \right] \\
&= 1 + \sum_{i=1}^{k-1} \binom{N_o + 1}{i} = \sum_{i=0}^{k-1} \binom{N_o + 1}{i}
\end{aligned}
$$

<br>

The proof is completed. the Saure's lemma is true for all $N$ and $k$. We finally arrive at the following inequality: 

<br>

$$
m_{\mathcal{H}}(N) \leq B(N, K) \leq  \sum_{i=0}^{k-1} \binom{N}{i}
$$

<br>

for all $N$. The right-hand side is polynominal in $N$ of degree $k-1$. We can now say that the growth function is a polynomial. Let's take some examples which we discussed in [Lecture 5](https://isopink.github.io/Effective-number-of-hypothesis/), and apply what we proved. 

<br>

##### 1.1. Positive rays 

The break point is $k=2$, and the growth function was *N+1*. You can recognize the following statement is true. 

<br>

$$
N+1 \leq \sum_{i=0}^{1} \binom{N}{i}
$$

<br>

##### 1.2. Positive intervals

The break point is $k=3$, and the growth function was *$\frac{1}{2}N^2 + \frac{1}{2}N + 1$*. You can recognize the following statement is true. 

<br>

$$
\frac{1}{2}N^2 + \frac{1}{2}N + 1 \leq \sum_{i=0}^{2} \binom{N}{i}
$$

<br>

##### 1.3. 2D perceptrons

The break point is $k=4$, and we don't know the growth funtion. However, You can bound the growth funtion as following statement:

<br>

$$
m_{\mathcal{H}}(N) \leq \frac{1}{6}N^3 + \frac{5}{6}N + 1
$$

<br>


