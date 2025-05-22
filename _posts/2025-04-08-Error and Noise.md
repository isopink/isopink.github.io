---
layout: single
title: "Lecture 4 : Error and Noise"
---

In this time, we will discuss about error and noise  it will be used for deeper concepts later. The discussion will proceed in the following three parts :

1. Error measures

2. Noisy targets

---

#### 1. Error measures 

When can we say that our hypothesis approximates the target funtion well? In other words, what does $h \approx f$ means? 
we need to define an error measure that qunatifies how far we are from the target funtion. Let's formalize the notion first: 

<br>

$$
\text{Error} = E(h, f).
$$

<br>

 It is almost always defined based on pointwise. - the individual input points $x$. if we define point wise error measure $e(h(x),f(x)$, the overall error will be the average value of pointwise errors. We now update the notation. 

<br>

$$
E_{\text{in}}(h) = \frac{1}{N} \sum_{n=1}^{N} e\left(h(\mathbf{x}_n), f(\mathbf{x}_n)\right)
$$

<br>

$$
E_{\text{out}}(h) = \mathbb{E}_{\mathbf{x}} \left[ e\left(h(\mathbf{x}), f(\mathbf{x})\right) \right]
$$

<br>

We already discussed the *in - sample error* in [__previous time__](https://isopink.github.io/Is-Learning-Feasible/). You may ask how to calculate *the out-of-sample error*. We will discuss it later. For now on, we just keep going. **The important thing is that the error measure can vary depending on the context**.  Consider the problem of verifying fingerpint belongs to a particular person. There are two types of error that our hypothesis make here. 

