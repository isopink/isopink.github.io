---
layout: single
title: "Lecture 11 : Overfitting"
---

In this time, we will discuss the concept of overfitting and the way to deal with it. The discussion will proceed in the following four parts: 

1. What is overfitting?

2. The role of noise

3. Deterministic noise

4. Dealing with overfitting

---

#### 1. What is overfitting? 

Overfitting occurs when a learning model fits the observed (training) data too well—typically because it is too complex or has too much degree of freedom—resulting in poor performance on new (test) data. Let me introduce a simple example. 

![solution](/assets/images/nn_1.svg) 

If data comes from a noisy quadratic target function and we use a 4th-degree polynomial to perfectly fit 5 points, $E_{\text{in}}$ could becomes zero—but $E_{\text{out}}$ could be huge. 


