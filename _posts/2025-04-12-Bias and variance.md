---
layout: single
title: "Lecture 8 : Bias-Variance Tradeoff"
---

In this time, we will discuss about bias and variace. At the end of the [Lecture 7](https://isopink.github.io/VC-Dimension/), we discussed Approximation-Generalization Tradeoff, with persepective of VC dimension. We now introuduce the new way. The new way provides a different angle, instead of bounding $E_{\text{out}}$ by $E_{\text{in}}$ plus term $\Phi$. We will decompose $E_{\text{out}}$ into two different error terms. The discussion will proceed in following two parts: 

1. Bias and Variance

2. Learning curves

---

#### 1. Bias and Variance 

So far, our main focus was reducing $E_{\text{out}}$, Which means a good approximation of $f$ out of sample. However, there was a tradeoff. More complex models(higher VC dimension) help $E_{\text{in}}$ but it hurts $\Phi$(Harder to generalize). Here is a friendly figure: 

![solution](/assets/images/bav_1.svg)

