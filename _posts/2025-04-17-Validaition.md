---
layout: single
title: "Lecture 13 : Validation"
---

This time, we will discuss **validation**, a powerful and practical tool to estimate out-of-sample error and control overfitting. The discussion will proceed in the following four parts:

1. Out-of-sample error and estimation  
2. Validation set approach  
3. Cross-validation  
4. Bias and variance of validation

---

#### 1. Out-of-sample error and estimation

In supervised learning, we ultimately care about how well a hypothesis performs on **unseen data**. That is, we want to minimize the out-of-sample error $E_{\text{out}}$.

However, in practice, we only have access to training data, so we cannot directly compute $E_{\text{out}}$. Instead, we look for good **estimates** of $E_{\text{out}}$ to guide our learning and model selection.

<br>

##### The three key errors:

| Error Type         | Symbol         | Description                                            |
|--------------------|----------------|--------------------------------------------------------|
| In-sample error    | $E_{\text{in}}$ | Error on training data                                 |
| Validation error   | $E_{\text{val}}$| Error on separate validation data                      |
| Out-of-sample error| $E_{\text{out}}$| True generalization error (on unseen test data)        |

<br>

We typically use $E_{\text{val}}$ as a **proxy** for $E_{\text{out}}$. The goal is to **predict $E_{\text{out}}$ without having to use test data**.

---

#### 2. Validation set approach

The simplest approach is to split the data $\mathcal{D}$ into two disjoint sets:

- **Training set**: used to train the model  
- **Validation set**: used to estimate $E_{\text{out}}$

![validation](/assets/images/val_1.svg)

Let the number of total data points be $N$, and validation set size be $K$. After splitting:

- Train $g^{(\mathcal{D}_{\text{train}})}$ on $N - K$ data points  
- Compute validation error on remaining $K$ data points:

<br>

$$
E_{\text{val}}(g) = \frac{1}{K} \sum_{n=1}^{K} \ell(g(\mathbf{x}_n), y_n)
$$

<br>

where $\ell$ is the loss function (e.g., squared loss or 0–1 loss).

This gives an **unbiased** estimate of $E_{\text{out}}$ — on average:

<br>

$$
\mathbb{E}_{\mathcal{D}_{\text{val}}}[E_{\text{val}}(g)] = \mathbb{E}[E_{\text{out}}(g)]
$$

<br>

However, this comes at a cost — fewer data points are used for training, which may reduce the model quality.

---

#### 3. Cross-validation

To address the trade-off between training size and validation size, we use **cross-validation**, especially when the dataset is small.

<br>

##### K-fold cross-validation:

1. Split data into $K$ equal-sized subsets (folds).  
2. For each fold $k = 1, \dots, K$:  
 a. Use fold $k$ as the validation set  
 b. Use remaining $K - 1$ folds as the training set  
3. Average the validation errors:

<br>

$$
E_{\text{cv}} = \frac{1}{K} \sum_{k=1}^{K} E_{\text{val}}^{(k)}
$$

<br>

This allows every data point to be used for both training and validation, just not in the same round. When $K = N$, this is called **Leave-One-Out Cross-Validation (LOOCV)**.

<br>

##### Trade-offs of K-fold:

| $K$          | Pros                            | Cons                                |
|--------------|----------------------------------|--------------------------------------|
| Small ($K=3$)| Fast computation                | High bias in $E_{\text{cv}}$         |
| Large ($K=10$ or $N$) | Low bias in estimate        | Expensive computation               |

Cross-validation is widely used in model selection, especially when comparing models with different complexities (e.g., polynomial degree, regularization strength $\lambda$, number of hidden units, etc.)

---

#### 4. Bias and variance of validation

Although $E_{\text{val}}$ is an **unbiased** estimate of $E_{\text{out}}$, it can have **high variance**, especially when $K$ is small (i.e., the validation set is small).

Let us consider:

<br>

$$
g = \arg\min_{g_m \in \mathcal{H}} E_{\text{val}}(g_m)
$$

<br>

That is, we select the model that performs best on the validation set. But **this selection itself introduces a bias** because we choose $g$ **after seeing** validation errors.

This results in **optimistic bias** in estimating $E_{\text{out}}(g)$ using $E_{\text{val}}(g)$. The more models we compare, the more likely it is that one of them will overfit the validation set.

<br>

##### Variance of validation estimate

The variance of $E_{\text{val}}$ for a fixed model $g$ depends on the loss function and validation set size $K$. For squared loss, variance decreases as $1/K$:

<br>

$$
\text{Var}(E_{\text{val}}(g)) = \frac{1}{K} \text{Var}(e(g(\mathbf{x}), y))
$$

<br>

So, using a **larger validation set** reduces variance, but it also reduces the training size. This is a fundamental trade-off in validation.

---

#### Summary

Validation is an essential technique in machine learning for estimating out-of-sample performance and for selecting models. Here's the recap:

<br>

| Method            | Goal                        | Strengths                              | Weaknesses                        |
|------------------|-----------------------------|----------------------------------------|-----------------------------------|
| Validation set   | Estimate $E_{\text{out}}$   | Simple, fast                           | Training set is smaller           |
| Cross-validation | Estimate and compare models | More accurate, uses all data           | Computationally expensive         |
| Leave-one-out    | Minimize bias               | Unbiased, low bias                     | Very high computation             |

Validation prevents us from fooling ourselves by using $E_{\text{in}}$ alone. But we must also be cautious about the bias introduced when selecting models based on validation error.

We will explore a more robust approach for this in the next session: **Validation with training/validation/test splits and early stopping**.

