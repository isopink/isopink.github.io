---
layout: single
title: "Lecture 13 : Validation"
---

This time, we will discuss **validation**, a powerful and practical tool to estimate $E_{\text{out}}$ and control overfitting. The discussion will proceed in the following three parts:

1. The validation set  
2. Model selection  
3. Cross-validation  

---

#### 1. The validation set 

So far, we described $E_{\text{out}}$ as below: 

<br>

$$
E_{\text{out}}(h) = E_{\text{in}}(h) + \text{overfit penalty}
$$

<br>

Our goal in [regularization](https://isopink.github.io/Regularization/) was to estimate the overfit penalty. In contrast, validation aims to estimate $E_{\text{out}}(h)$ directly using a validation set. A validation set is similar to a test set in that it’s held out from training and used to estimate out-of-sample error. Unlike a test set, it can influence model selection—but this influence is minor, so the estimate of $E_{\text{out}}$ remains reliable.

Let us look at how the validation set is created. First, pick $K$ samples from $\mathcal{D}$ to make $\mathcal{D}_{\text{val}}$. Then, let the remaining $N-K$ data points, training data, $\mathcal{D}


