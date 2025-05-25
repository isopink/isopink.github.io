---
layout: single
title: "Lecture 8 : Bias-Variance Tradeoff"
---

In this time, we will discuss about bias and variace. At the end of the [Lecture 7](https://isopink.github.io/VC-Dimension/), we discussed Approximation-Generalization Tradeoff, with persepective of VC dimension. We now introuduce the new way of analysing model. The discussion will proceed in following two parts: 

1. Bias and Variance

2. Learning curves

---

#### 1. Bias and Variance 

So far, our main focus was reducing $E_{\text{out}}$, which means a good approximation of $f$ out of sample. To do so, We bounded $E_{\text{out}}$ by $E_{\text{in}}$ plus term $\Phi$. However, Bias-Variance analysis decomposes $E_{\text{out}}$ into two things: 

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

Bias-Variance decomposition of $E_{\text{out}}$ can be applied to targets with real-values, and uses squared error. We start with representation of $E_{\text{out}}$:

<br>  

$$
E_{\text{out}}(g^{(\mathcal{D})}) = \mathbb{E}_{\mathbf{x}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - f(\mathbf{x}) \right)^2 \right]  
$$

<br>

If we denote a randomly given dataset as $\mathcal{D}$, then $g^{(\mathcal{D})}$ can be defined as the final hypothesis $g$ obtained from the dataset $D$. We have made explicit the dependence of the final hypothesis $g$ on the data $\mathcal{D}$. We can rid of the dependence on a particular data set by taking the expectation with respect to all data sets. Then the formula becomes: 

<br>

$$
\mathbb{E}_{\mathcal{D}} \left[ E_{\text{out}}(g^{(\mathcal{D})}) \right] = \mathbb{E}_{\mathcal{D}} \left[ \mathbb{E}_{\mathbf{x}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - f(\mathbf{x}) \right)^2 \right] \right]  
$$

<br>

By Fubini's theorem, We can state the formula as: 

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

Let $\bar{g}(\mathbf{x}) = \mathbb{E}_{\mathcal{D}} \left[ g^{(\mathcal{D})}(\mathbf{x}) \right]$. Using $\bar{g}$, with few techniques, our formula becomes: 

<br>

$$
\mathbb{E}_{\mathcal{D}} \left[ \left( g^{(\mathcal{D})}(\mathbf{x}) - \bar{g}(\mathbf{x}) \right)^2 \right] 
+ \left( \bar{g}(\mathbf{x}) - f(\mathbf{x}) \right)^2
$$

<br>

The term $(\bar{g}(\mathbf{x}) - f(\mathbf{x}))^2$ measures how much the average function that we would learn using different data sets $\mathcal{D}$ deviates from the target function that generated these data sets. This term is appropriately called the bias:

<br>

$$
\text{bias}(\mathbf{x}) = \left( \bar{g}(\mathbf{x}) - f(\mathbf{x}) \right)^2,
$$

<br>


