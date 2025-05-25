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
m_{\mathcal{H}}(N) \leq \sum_{i=0}^{3} \binom{N}{i} = \frac{1}{6}N^3 + \frac{5}{6}N + 1
$$

<br>

---

#### 2. Proof that $m_{\mathcal{H}}(N)$ can replace $M$.

<br>

$$
\mathbb{P}\left[\, \left| E_{\text{in}}(g) - E_{\text{out}}(g) \right| > \epsilon \,\right] \leq 2M \, e^{-2\epsilon^2 N}
$$

<br>

This was the Union bound form. But if the $M$ goes larger, the inequality goes useless. To get around this issue, We want to replace $M$. That was our goal. 
Unfortunately, We cannot just put  $m_{\mathcal{H}}(N)$ to the position of $M$. Instead, we use:

<br>

$$
\mathbb{P}\left[\, \left| E_{\text{in}}(g) - E_{\text{out}}(g) \right| > \epsilon \,\right] \leq 4 \, m_{\mathcal{H}}(2N) \, e^{-\frac{1}{8} \epsilon^2 N}
$$

<br>

This is the *VC Inequality* or *VC bound*. It is the most imporatnt mathematical result in the theory of learning. Since the formal proof is lengthy and technical. I will illustrate the main ideas in a sketch of the proof, and iclude the formal proof as an apprendix. 

![solution](/assets/images/tog_1.svg)

For a given hypothesis $h \in \mathcal{H}$, the event “$\left| E_{\text{in}}(h) - E_{\text{out}}(h) \right| \geq \epsilon$" consists of all points $\mathcal{D}$ for which the statement is true. For a particular $h$, let us paint all these ‘bad’ points using one color. What the basic Hoeffding Inequality tells us is that the colored area on the canvas will be small.

![solution](/assets/images/tog_2.svg)

Each hypothesis $h \in \mathcal{H}$ may cause a different set of points where $|E_{\text{in}}(h) - E_{\text{out}}(h)| \geq \epsilon$. The union bound adds up all these areas without considering overlaps, leading to a loose bound when $\mathcal{H}$ is large.

![solution](/assets/images/tog_3.svg)

The bulk of the VC Inequality proof deals with how to account for the overlaps. Here is the idea. If you were told that the hypotheses in $\mathcal{H}$ are such that each point on the canvas that is colored will be colored 100 times (because of 100 different $h$’s), then the total colored area is now 1/100 of what it would have been if the colored points had not overlapped at all. This is the essence of the VC bound as illustrated. 

The bulk of the VC proof deals with how to account for the overlaps. Here is the idea. If you were told that the hypotheses in $\mathcal{H}$ are such that each point on the canvas that is colored will be colored 100 times (because of 100 different $h$’s), then the total colored area is now 1/100 of what it would have been if the colored points had not overlapped at all. This is the essence of the VC bound as illustrated. 

<br>

##### Extra!

There is one more thing to consider. The reason $m_{\mathcal{H}}(2N)$ appears in the VC bound instead of $m_{\mathcal{H}}(N)$ is that the proof uses a sample of $2N$ points instead of $N$ points. Why do we need $2N$ points? The event “$\left|E_{\text{in}}(h) - E_{\text{out}}(h)\right| > \epsilon$” depends not only on $D$, but also on the entire $\mathcal{X}$ because $E_{\text{out}}(h)$ is based on $\mathcal{X}$. This breaks the main premise of grouping $h$’s based on their behavior on $D$, since aspects of each $h$ outside of $D$ affect the truth of “$\left|E_{\text{in}}(h) - E_{\text{out}}(h)\right| > \epsilon$.” 

To remedy that, we consider the artificial event “$\left|E_{\text{in}}(h) - E_{\text{in}}'(h)\right| > \epsilon$” instead, where $E_{\text{in}}$ and $E_{\text{in}}'$ are based on two samples $D$ and $D'$ each of size $N$. This is where the $2N$ comes from. It accounts for the total size of the two samples $D$ and $D'$. Now, the truth of the statement “$\left|E_{\text{in}}(h) - E_{\text{in}}'(h)\right| > \epsilon$” depends exclusively on the total sample of size $2N$, and the above redundancy argument will hold.

Of course we have to justify why the two-sample condition “$\left|E_{\text{in}}(h) - E_{\text{in}}'(h)\right| > \epsilon$” can replace the original condition “$\left|E_{\text{in}}(h) - E_{\text{out}}(h)\right| > \epsilon$.” In doing so, we end up having to shrink the $\epsilon$’s by a factor of 4, and also end up with a factor of 2 in the estimate of the overall probability. This accounts for the $\frac{8}{N}$ instead of $\frac{1}{2N}$ in the VC bound and for having 4 instead of 2 as the multiplicative factor of the growth function. When you put all this together, you get the formula. 

