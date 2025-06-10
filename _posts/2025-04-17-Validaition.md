---
layout: single
title: "Lecture 13 : Validation"
---

In this time, we will discuss **validation**, a powerful and practical tool to estimate $E_{\text{out}}$ and control overfitting. The discussion will proceed in the following three parts:

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

Our goal in [regularization](https://isopink.github.io/Regularization/) was to estimate the overfit penalty. In contrast, validation aims to estimate $E_{\text{out}}(h)$ directly using a validation set. A validation set is similar to a test set in that it’s held out from training and used to estimate out-of-sample error. 


 ![solution](/assets/images/nn_1.svg) 


