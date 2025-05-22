---
layout: single
title: "Lectrue 6 : Theory of Generlization"
---

In this time, we will discuss the proof about [<u>$m_{\mathcal{H}}(N)$</u>](https://isopink.github.io/Effective-number-of-hypothesis/) The discussion will proceed in the following two parts :

1.Proof that mh(n) is polynominal

2. proof that mh(n) can replace m 


---

#### 1. Proof that $m_{\mathcal{H}}(N)$ is polynominal

Let $B(N,K)$ is the maximum number of dichotomies of $N$ points such that no subset of size $k$ of the $N$ points can be shattered by these dichotomies. Since $B(N,K)$ is defined as a maximu, it will serve as an upper bound for any $m_\mathcal{H}(N)$ that has a break point $k$: 

<br>

$$
m_{\mathcal{H}}(N) \leq B(N, k)
$$

<br>

**If we show $B(N,K) \leq \text{Polynominal}$, the game is over.** Let's get it started. I listed these dichotomies of $B(N,K)$ in the follownig table: 

<br>

$$
\begin{array}{|c|c|c c c c|c|}
\hline
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
\hline
\end{array}
$$

<br>




