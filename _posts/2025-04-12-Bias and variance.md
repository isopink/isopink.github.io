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

