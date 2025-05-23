---
layout: single
title: "Lecture 7 : VC dimension"
---

In this time, we now introduce the **VC dimension**. At the end of the last session, we introduced *VC bound*. We will dive into that topic. The discussion will proceed in following four parts: 

1. The difinition of VC diemnsion

2. VC dimension of perceptrons

3. Interpreting the VC dimension

4. Generalization bounds

---

#### 1. The difinition of VC dimension

If you rememeber the difition of *break point*, which we learnd in [<u>Lecture 5</u>](https://isopink.github.io/Effective-number-of-hypothesis/), you can easily accept the difinition of VC dimension. The *Vapnik–Chervonenkis dimension* of a hypothesis set $\mathcal{H}$, denoted by $d_{\text{VC}}(\mathcal{H})$ or simply $d_{\text{VC}}$, is the largest value of $N$ for which $ m_{\mathcal{H}}(N) = 2^N.$ 

If $d_{\text{VC}}$ is the VC dimension of $\mathcal{H}$, then **$k = d_{\text{VC}} + 1$** is a break point for $m_{\mathcal{H}}$, since $m_{\mathcal{H}}(N)$ cannot equal $2^N$ for any $N > d_{\text{VC}}$ by definition. Since $k = d_{\text{VC}} +1$, our previous *Growth funtion* with polynominal bound can be rewritten as : 

<br>

$$
m_{\mathcal{H}}(N) \leq \sum_{i=0}^{k-1} \binom{N}{i} = \sum_{i=0}^{d_\text{VC}} \binom{N}{i}
$$

<br>




