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

Let us contrast validation with regularization first, when overfitting is concerned. $E_{\text{out}}$ can be expressed as below: 

<br>

$$
E_{\text{out}}(h) = E_{\text{in}}(h) + \text{overfit penalty}
$$

<br>

This tells us that $E_{\text{in}}$ is not exactly $E_{\text{out}}$. The more complex the model, the bigger the overfit penalty. So, what does regularizaiton do? 

<br>

$$
E_{\text{out}}(h) = E_{\text{in}}(h) + \underbrace{\text{overfit penalty}}_{\text{regularization estimates this quantity}}
$$

<br>




 ![solution](/assets/images/nn_1.svg) 


