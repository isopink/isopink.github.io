---
layout: single
title: "Lecture 11 : Overfitting"
---

In this time, we will discuss the concept of overfitting and the way to deal with it. The discussion will proceed in the following four parts: 

1. What is overfitting?

2. Reason of overfitting

3. Deterministic noise

4. Dealing with overfitting

---

#### 1. What is overfitting? 

Overfitting occurs when a learning model fits the observed (training) data too well—typically because it is too complex or has too much degree of freedom—resulting in poor performance on new (test) data. This is the result of fitting the noise in the data. Let me introduce a simple example. 

![solution](/assets/images/of_1.svg) 

If the data comes from a noisy quadratic function and we use a 4th-degree polynomial to perfectly fit 5 points, $E_{\text{in}}$ may be zero, but $E_{\text{out}}$ can be large. This goes beyond just bad [generalization](https://isopink.github.io/VC-Dimension/)—it is overfitting, where the process of picking a hypothesis with lower $E_{\text{in}}$ ends up increasing $E_{\text{out}}$. 

---

#### 2. Reason of overfitting

Let us dig deeper to gain a better understanding of when overfitting occurs. Consider the two regression problems below: 

![solution](/assets/images/of_2.svg)

In both problems, the target function is a polynomial and the data set $D$ contains 15 data points. In (a), the target function is a 10th order polynomial and the sampled data are noisy. In (b), the target function is a 50th order polynomial and the data are noiseless. The best 2nd and 10th order fits are shown in next figure: 

![solution](/assets/images/of_3.svg)

Here are the table of $E_{\text{in}}$ and $E_{\text{out}}$. 

<br>

|                      | **10th Order Noisy Target** |           | **50th Order Noiseless Target** |           |
|----------------------|-----------------------------|-----------|----------------------------------|-----------|
|                      | 2nd Order                  | 10th Order | 2nd Order                       | 10th Order |
| $E_{\text{in}}$      | 0.050                      | 0.034      | 0.029                           | $10^{-5}$  |
| $E_{\text{out}}$     | 0.127                      | **9.00**   | 0.120                           | **7680**   |

<br>

Surprisingly, the 2nd order model performed significantly better than the 10th order polynomial model in both examples. The 10th order fits have lower $E_{\text{in}}$ and higher $E_{\text{out}}$. This is indeed a case of overfitting that results in pathologically bad generalization. Let us take a look at these two cases one by one. 

<br>

##### 2.1. 10th Order Noisy Target

![solution](/assets/images/of_4.svg)

Using a 10th-order model on 10th order target function doesn’t seem excessive. In fact, using a 2nd-degree model might seem too simple. So why did this happen? This is because of the quality of the data. The model learned not only the pure data, but also the noisy data. 

Furthermore, qunatity of data is also matter. As we discussed in [Lecture 7](https://isopink.github.io/VC-Dimension/), proper learning requires about ten times the VC dimension in data. Thr 2nd order model needs around 30 points, while a 10th order model needs about 110. Although the data was insufficient for both, it was closer to what's needed for the 2nd model, which explains its better performance. Actually, we have seen this case [before](https://isopink.github.io/Bias-and-variance/). 

![solution](/assets/images/of_5.svg)

With enough data, the 10th order model ​would outperform the 2nd order model. But with limited data, as in this case, the 2nd model performs better due to its smaller gap between $E_{\text{in}}$ and $E_{\text{out}}$.

<br>

##### 2.2. 50th Order Noiseless target 

We have discussed that noisy data could occur overfitting. Then, if the the data is noiseless, can we find the exact target function? Maybe not. Here is our second example about 50th order target:

![solution](/assets/images/of_6.svg)

Despite the noiseless of data, 10th order model heavily overfits the data. The 2nd order model wins. This is because the complexity of the target function. 

<br>

##### 2.3. The overfit measure 

With the inspection of (2.1) and (2.2) we can realize what matters is how the model complexity matches the quantity and quality of the data we have, not how it matches the target function. One can think the overfitting can be influenced by the noise level, the amount of data, and the complexity of the target function. We will explore this idea through the following experiment. 

Let $x \in \mathbb{R}$ be the input and $y$ the output. Without noise:

<br>

$$
y = f(x)
$$

<br>

With additive noise $\epsilon(x) \sim \mathcal{N}(0, \sigma^2)$, the observed output becomes:

<br>

$$
y = f(x) + \epsilon(x)
$$

<br>

Assume $f(x)$ is a polynomial of degree $Q_f$, and let $N$ be the number of data points. 

![solution](/assets/images/of_7.svg)

The figure above illustrate the case where $Q_f =10$, $N=15$, and the noise variance $\sigma^2$. We compare the final hypothesis $g_{10} \in \mathcal{H}_{10}$ (larger model) to the final hypothesis $g_2 \in \mathcal{H}_2$ (smaller model). Clearly, $E_{\text{in}}(g_{10}) \leq E_{\text{in}}(g_2)$ since $g_{10}$ has more degrees of freedom to fit the data. What is surprising is how often $g_{10}$ overfits the data, resulting in $E_{\text{out}}(g_{10}) > E_{\text{out}}(g_2)$.  

Let us define the overfit measure as: 

$$
E_{\text{out}}(g_{10}) - E_{\text{out}}(g_2)
$$

The more positive this measure is, the more severe overfitting would be.



