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

Our goal in [regularization](https://isopink.github.io/Regularization/) was to estimate the overfit penalty. In contrast, validation aims to estimate $E_{\text{out}}(h)$ directly using a validation set. A validation set is similar to a test set in that it’s held out from training and used to estimate out-of-sample error. Unlike a test set, it can influence model selection—but this influence is minor, so the estimate of $E_{\text{out}}$ remains reliable.

Let us first look at how the validation set is created. First, pick $N-K$ samples from $\mathcal{D}$ to make the training set:

<br>

$$
\mathcal{D}_{\text{train}}
$$

Then, let the remaining $K$ data points be the validation set:

<br>

$$
\mathcal{D}_{\text{val}}
$$

Now, we run the learning algorithm using $\mathcal{D}_\{text{train}}$ to obtain a final hypothesis $g^{-} \in \mathcal{H}$, where the 'minus' superscript indicates that some data points were taken out of training. We then compute the validation error for $g^{-}$ using the validaition set: 

<br>

$$
E_{\text{val}}(g^-) = \frac{1}{K} \sum_{\mathbf{x}_n \in \mathcal{D}_{\text{val}}} e\left(g^-(\mathbf{x}_n), y_n\right)
$$

<br>

$E_{\text{val}}$ is an unbiased estimate of $E_{\text{out}}$ since the final hypothesis $g^{-}$ was created independently of the the $\mathcal{D}_{\text{val}}$. We can desribe this fact as: 

<br>

$$
\begin{aligned}
\mathbb{E}_{\mathcal{D}_{\text{val}}} \left[ E_{\text{val}}(g^-) \right] 
&= \frac{1}{K} \sum_{\mathbf{x}_n \in \mathcal{D}_{\text{val}}} \mathbb{E}_{\mathcal{D}_{\text{val}}} \left[ e\left(g^-(\mathbf{x}_n), y_n\right) \right] \\ \\
&= \frac{1}{k} \sum_{\mathbf{x}_n \in \mathcal{D}_{\text{val}}} \mathbb{E}_{\mathbf{x}_n} \left[ e\left(g^-(\mathbf{x}_n), y_n\right) \right] \\ \\
&= \frac{1}{K} \sum_{\mathbf{x}_n \in \mathcal{D}_{\text{val}}} E_{\text{out}}(g^-) \\ \\
&= E_{\text{out}}(g^-)
\end{aligned}
$$

<br>

 


