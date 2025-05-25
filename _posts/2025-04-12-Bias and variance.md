---
layout: single
title: "Lecture 8 : Bias-Variance Tradeoff"
---

In this post, we will discuss bias and variance. At the end of [Lecture 7](https://isopink.github.io/VC-Dimension/), we discussed the Approximation-Generalization Tradeoff from the perspective of the VC dimension. We now introduce a new way to analyze models. The discussion will proceed in the following two parts: 

1. Bias and Variance  
2. Learning Curves  

---

#### 1. Bias and Variance 

So far, our main focus was reducing $E_{\text{out}}$, which means a good approximation of $f$ out of sample. To do so, we bounded $E_{\text{out}}$ by $E_{\text{in}}$ plus a term $\Phi$. However, bias-variance analysis decomposes $E_{\text{out}}$ into two components: 

<div align="center">

<br>  

$$
1.\ \text{How well } \mathcal{H} \text{ can approximate } f  
$$

<br>

$$
2.\ \text{How well we can zoom in on a good } h \in \mathcal{H}  
$$

<br>

</div>

Bias-variance decomposition of $E_{\text{out}}$ can be applied to targets with real values and uses squared error. We start with the expression for $E_{\text{out}}$:

<br>  

$$
E_{\text{out}}(g^{(\mathcal{D})}) = \mathbb{E}_{\mathbf{x}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - f(\mathbf{x}) \right)^2 \right]  
$$

<br>

If we denote a randomly given dataset as $\mathcal{D}$, then $g^{(\mathcal{D})}$ can be defined as the final hypothesis $g$ obtained from the dataset $\mathcal{D}$. We have made explicit the dependence of the final hypothesis $g$ on the data $\mathcal{D}$. We can remove the dependence on a particular data set by taking the expectation with respect to all data sets. Then the formula becomes: 

<br>

$$
\mathbb{E}_{\mathcal{D}} \left[ E_{\text{out}}(g^{(\mathcal{D})}) \right] = \mathbb{E}_{\mathcal{D}} \left[ \mathbb{E}_{\mathbf{x}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - f(\mathbf{x}) \right)^2 \right] \right]  
$$

<br>

By Fubini's theorem, we can write the formula as: 

<br>

$$
\mathbb{E}_{\mathbf{x}} \left[ \mathbb{E}_{\mathcal{D}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - f(\mathbf{x}) \right)^2 \right] \right]  
$$

<br>

Now, let us focus on:

<br>

$$  
\mathbb{E}_{\mathcal{D}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - f(\mathbf{x}) \right)^2 \right]  
$$

<br>

Let $\bar{g}(\mathbf{x}) = \mathbb{E}_{\mathcal{D}} \left[ g^{(\mathcal{D})}(\mathbf{x}) \right]$. Using $\bar{g}$ and some algebra, our formula becomes: 

<br>

$$
\mathbb{E}_{\mathcal{D}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - \bar{g}(\mathbf{x}) \right)^2 \right] 
+ \left( \bar{g}(\mathbf{x}) - f(\mathbf{x}) \right)^2
$$

<br>

The term $(\bar{g}(\mathbf{x}) - f(\mathbf{x}))^2$ measures how much the average hypothesis that we would learn using different data sets $\mathcal{D}$ deviates from the target function that generated these data sets. This term is called the bias:

<br>

$$
\text{bias}(\mathbf{x}) = \left( \bar{g}(\mathbf{x}) - f(\mathbf{x}) \right)^2,
$$

<br>

The other term measures how far a specific hypothesis in the hypothesis set is from the average hypothesis. In other words, this term can be interpreted as an indicator of how spread out the hypotheses are. This term is called the variance:

<br>

$$
\text{var}(\mathbf{x}) = \mathbb{E}_{\mathcal{D}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - \bar{g}(\mathbf{x}) \right)^2 \right],
$$

<br>

We thus arrive at the bias-variance decomposition of $E_{\text{out}}$: 

<br>

$$
\mathbb{E}_{\mathcal{D}}\left[ E_{\text{out}}(g^{(\mathcal{D})}) \right] 
= \mathbb{E}_{\mathbf{x}} \left[ \text{bias}(\mathbf{x}) + \text{var}(\mathbf{x}) \right]
$$

<br>

The approximation-generalization tradeoff is captured in the bias-variance decomposition. To illustrate, let’s consider two extreme cases: a very small model (with one hypothesis) and a very large one with all hypotheses. 

![solution](/assets/images/bav_1.svg) 

The figure on the left represents an extreme case where there is only a single final hypothesis $g^{(D)}$ within the entire hypothesis set $\mathcal{H}$, and that hypothesis itself becomes the average $\bar{g}$. In this case, the distance between the point $\bar{g}$ and the target function $f$ becomes the bias. Since there is only one point, the variance is zero.

![solution](/assets/images/bav_1.5svg) 

The figure on the right shows a large hypothesis set $\mathcal{H}$ that includes the target function $f$. The average hypothesis $\bar{g}$ is close to $f$, so the bias is nearly zero. However, the hypotheses are widely spread around $\bar{g}$, leading to high variance.

In conclusion, there is a tradeoff between bias and variance. As the hypothesis set $\mathcal{H}$ becomes larger, bias decreases and variance increases. Let us see one more example with a sinusoid.  

![solution](/assets/images/bav_2.svg)

Consider a target function $f(x) = \sin(\pi x)$ and a data set of size $N=2$. We sample $x$ uniformly in $[-1, 1]$ to generate a data set $ (x_1, y_1), (x_2, y_2); $ and fit the data using one of two models: 

<br>

$$
\mathcal{H}_0:\quad h(x) = b  
$$

<br>

$$  
\mathcal{H}_1:\quad h(x) = ax + b  
$$

<br>

Which one is the better hypothesis? We have to establish the criteria first. In general, we prefer lower $E_{\text{out}}$. And we have learned bias-variance decomposition. We shall apply this method here. 

For $\mathcal{H}_0$, we choose the constant hypothesis that best fits the data (the horizontal line at the midpoint, $b = \frac{y_1 + y_2}{2}$). For $\mathcal{H}_1$, we choose the line that passes through the two data points $(x_1, y_1)$ and $(x_2, y_2)$. Repeating this process with many data sets, we can estimate the bias and the variance. The figures which follow show the resulting fits on the same (random) data sets for both models.

![solution](/assets/images/bav_3.svg)

With $\mathcal{H}_1$, the learned hypothesis is more sensitive and varies significantly depending on the data set. The bias-variance analysis is summarized in the next figures.

![solution](/assets/images/bav_4.svg)

We can find that the sum of bias and variance is much larger in $\mathcal{H}_1$. That is to say, we should consider $\mathcal{H}_0$ as the better hypothesis. However, this is not intuitively satisfying. $\mathcal{H}_1$ seems to approximate the sine function better. Why does this result go against our intuition? 

It's because model complexity should be defined based on the data, not on how complex the target function is. In the previous example, the data consisted of only two points. With just two points, the set of possible functions is very limited, so the simpler model $\mathcal{H}_0$ performed better. However, if we are given more points for the same target function, the more complex model $\mathcal{H}_1$ would perform better.

---

#### 2. Learning Curves 

This time, we will look at how the in-sample error and out-of-sample error behave as the size of the data set increases. After learning with a particular data set $\mathcal{D}$ of size $N$, the final hypothesis $g^{(\mathcal{D})}$ has in-sample error $E_{\text{in}}(g^{(\mathcal{D})})$ and out-of-sample error $E_{\text{out}}(g^{(\mathcal{D})})$, both of which depend on $\mathcal{D}$. 

As we saw in the Bias-Variance analysis, the expectation with respect to all data sets of size $N$ gives the expected errors: 

<br>

$$
\mathbb{E}_{\mathcal{D}} \left[ E_{\text{in}}(g^{(\mathcal{D})}) \right] \quad \text{and} \quad \mathbb{E}_{\mathcal{D}} \left[ E_{\text{out}}(g^{(\mathcal{D})}) \right]
$$

<br>

These expected errors are functions of $N$, and are called the learning curves of the model. We illustrate the learning curves for a simple learning model and a complex one. 

![solution](/assets/images/bav_5.svg)

For the simple model, the learning curves converge faster but to worse final performance. In both models, out-of-sample error decreases with $N$, while in-sample error increases. The complex model shows very low in-sample error for small $N$ because it can perfectly fit small data sets, as in the previous sine example. Let's now compare these curves using VC and bias-variance analysis.

![solution](/assets/images/bav_6.svg) 

In VC analysis, $E_{\text{out}}$ is bounded by $E_{\text{in}}$ plus a complexity penalty $\Omega$. In bias-variance analysis, it’s split into bias and variance. As $N$ increases, both $\Omega$ and variance decrease. The bias-variance view is idealized, assuming $\bar{g}$ performs as well as the best possible hypothesis.
