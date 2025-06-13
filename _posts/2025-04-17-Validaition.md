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

Regularizaiton tried to guess overfit penalty. Basically, we made up a term that we think represents the overfitting penalty. Now, to constrast this, What does validation do? 

<br>

$$
\underbrace{E_{\text{out}}(h)}_{\text{validation estimates this quantity}} = E_{\text{in}}(h) + \text{overfit penalty}
$$

<br>

Validation estimates $E_{\text{out}}$ directly. This is not completely a foreign idea to us, because we use a test set in order to do that. Let us stpend a few moment to describe the estimate. 

Consider we are given an out-of-sample point, $(\mathbf{x},y)$. We used to call it test point. Now, we are going to call it validation point. It won't be clear why we are naming it differently until we use the validation set later. We represent our error as:  

<br>

$$
e(h(\mathbf{x}), y)
$$

<br>

This could be a simple squared error, or binary error. We have seen these before. Now, if we take this qunatity as: 

<br>

$$
\mathbb{E} \left[ e(h(\mathbf{x}), y) \right] = E_{\text{out}}(h)
$$

<br>

This is an unbiased estimate of $E_{\text{out}}$ as its expected value over the distribution on $\mathbf{x}$ is simply $E_{\text{out}}$. And, the variance is: 

<br>

$$
\mathrm{Var} \left[ e(h(\mathbf{x}), y) \right] = \sigma^2
$$

<br>

We denote the variance as $\sigma^2$. However, since we are using only one point, the estimate will be poor because of high-variace. Therefore, we cannot rely on it to estimate $E_{\text{out}}$. To get around this issue, let us move on to a full set. Consider we are given validation set, size of $K$: 

<br>

$$
(\mathbf{x}_1, y_1), (\mathbf{x}_2, y_2), \cdots, (\mathbf{x}_K, y_K)
$$

<br>

And the error on that set, we are going to call it $E_{\text{val}}$ as in validaition error: 

<br>

$$
E_{\mathrm{val}}(h) = \frac{1}{K} \sum_{k=1}^{K} e(h(\mathbf{x}_k), y_k)
$$

<br>

What is expected value of $E_{\text{val}}$? We just take the expected value of above equation as below: 

<br>

$$
\mathbb{E} \left[ E_{\mathrm{val}}(h) \right] = \frac{1}{K} \sum_{k=1}^{K} \mathbb{E} \left[ e(h(\mathbf{x}_k), y_k) \right] = E_{\mathrm{out}}(h)
$$

<br>

So indeed, again, the validation error is an unbiased estimate of the out-of-sample error, provided that all you did with the validation set is just measure the out-of-sample error. Now, let us look at the variace, because that was our problem with the single-point estimate.

<br>

$$
\mathrm{Var} \left[ E_{\mathrm{val}}(h) \right] = \frac{1}{K^2} \sum_{k=1}^{K} \mathrm{Var} \left[ e(h(\mathbf{x}_k), y_k) \right] = \frac{\sigma^2}{K}
$$

<br>

With this inspection, we can define our estimated out-of-sample error as below: 

<br>

$$
E_{\mathrm{val}}(h) = E_{\mathrm{out}}(h) \pm \mathcal{O} \left( \frac{1}{\sqrt{K}} \right)
$$

<br>

The equation illustrates that the accuracy of our validation error $E_{\text{val}}(h)$ in estimating the true out-of-sample error $E_{\text{out}}(h)$ improves as the size of validation set $K$ grows. 

The interesting point is that $K$ is not free. Increasing $K$ is a good thing—but why don’t we just use more validation points? Because in practice, $K$ isn’t given to us in addition to the training set. So every time we take a point for validation, we are taking it away from training.
Let us examine this more precisely. Consider we are given data set $\mathcal{D}$ as: 

<br>

$$
\mathcal{D} = (\mathbf{x}_1, y_1),(\mathbf{x}_2, y_2), \cdots, (\mathbf{x}_N, y_N)
$$

<br>

We are going to take any random $K$ points as validation set. Then, we have $N-K$ points as training set. Now, let us recall the learning curve. 

 ![solution](/assets/images/val_1.svg) 

As $K$ increases, $N - K$ decreases, which can lead to a higher $E_{\text{out}}$. This is a price to be paid for $K$. It turns out that we are going to have a trick that will make us not pay that price. But still, the question of what happens when K is big is a question mark in our mind. Then, why don't we resotre the data set afterwe have the estimate? The situation is illustrated below: 

 ![solution](/assets/images/val_2.svg) 

If we used the full training set to train, we would get a final hypothesis, which we call $g$.  
But in the validation setting, we only train on $\mathcal{D}_{\text{train}}$. The resulting hypothesis is $g^-$, since it is trained on a smaller dataset. 

The trick is to use $g^-$ evaluated on $\mathcal{D}_{\text{val}}$ as a reliable proxy for $g$'s unknown performance. This allows us to then maximize $g$'s potential by training it on all data and ultimately report $g$ as our final hypothesis.

If $K$ is small, then the validation error for $g^-$ is similar to that for $g$, so it doesn't cause much of a problem. However, if $K$ is large, the gap between $g^-$ and $g$ becomes significant, making the validation error itself less meaningful.

In conclusion, as long as the size of the validation set is chosen properly, there is no issue in using the same data for both validation and training. As a rule of thumb, we suggests using about 20% of the total dataset as the validation set.

It seems nothing different from a test set. Then, why do we call it a validation set? It is because we use it to make choices. Consider Early Stopping in neural networks:

 ![solution](/assets/images/val_3.svg) 

If we simply observe performance on a dataset, it acts as a test set, yielding an unbiased estimate. However, the moment we make a decision based on those observations—like stopping training at the lowest error point—that dataset becomes a validation set. This "choice" introduces a bias, making the estimate optimistically skewed. Thus, using a set for active decisions changes its nature from a neutral test set to a biased validation set.

To understand Optimistic Bias more precisely, let us consider a simple example. Suppose we have two hypotheses, $h_1$ and $h_2$ with: 

<br>

$$
E_{\mathrm{out}}(h_1) = E_{\mathrm{out}}(h_2) = 0.5
$$

<br>

We estimate their errors as $e_1$ and $e_2$, and assume both are uniformly distributed between $0$ and $1$. Now, we pick the hypothesis with the smaller estimated error as below: 

<br>

$$
\text{Pick } h \in \{ h_1, h_2 \} \quad \text{with} \quad e = \min(e_1, e_2)
$$

<br>


Although both $e_1$ and $e_2$ are unbiased, the minimum of the two tends to be less than $0.5$ on average. We can describe this as below: 

<br>

$$
\mathbb{E}(e) < 0.5
$$

<br>

In fact, there's a $75\%$ chance that the smaller value is below $0.5$. This means the selected hypothesis looks better than it actually is— which is why we call this effect Optimistic Bias 

---

#### 2. Model selection 

Basically, we are going to use the validation set more than once. This is how we are going to make the choice. So let us first look at the full process diagram shown below: 

 ![solution](/assets/images/val_4.svg)

 Let us discuss how the diagram reflects the logic. Suppose we have $M$ different models: 
 
 <br>
 
 $$
 \mathcal{H}_1, \ldots, \mathcal{H}_M
 $$
 
 <br>
 
If we train each model using the dataset $\mathcal{D}_{\text{train}}$ (excluding the validation set), we obtain final hypotheses $g^-_m$ for each model. Now, suppose we evaluate each $g^-_m$ on the validation set.

$\mathcal{D}_{\text{val}}$ will measure their validation errors as:

<br>

$$
E_1, \ldots, E_M
$$

<br>

Among these, we select the model with the lowest validation error, say $E_{m^*}$, as the best-performing model. As previously discussed, this selection process may include Optimistic Bias.

Selecting the best hypothesis $H_{m^*}$ is no different in concept. However, this time we retrain it not on $\mathcal{D}_{\text{train}}$, but on the full dataset $\mathcal{D}$.

Using all available data, final hypothesis $g_{m^*}$ is then obtained from: 

<br>

$$ \mathcal{H}_{m^*}$$

<br>

This whole process is illustrated in our above diagram. Now, let us discuss more about bias. Consider following learning curve figure: 

![solution](/assets/images/val_5.svg)

We have two questions about the figure. First, why does $E_{\text{out}}$ increase as $K$ increases? This is because the size of the training set decreases as $K$ increases. Second, why does $E_{\text{out}}$ converge as $K$ increases? This is because our estimate of $E_{\text{val}}$ becomes more accurate with larger $K$, and also because the true out-of-sample error naturally increases due to smaller training sets.

Now let us formalize it. How much is the bias? When we select the best model using a validation set, we're effectively training on a special hypothesis set — the set of $M$ final models: 

<br>

$$
\mathcal{H}_{\text{val}} = \left\{ g_1^-,\ g_2^-,\ \ldots,\ g_M^- \right\}
$$


<br>

From the validation set’s perspective, it's simply choosing the one with the lowest error, like training on a small hypothesis space. We can formalize it with the [VC dimension](https://isopink.github.io/VC-Dimension/) as below: 

<br>

$$
E_{\text{out}}(g_{m^*}^-) \leq E_{\text{val}}(g_{m^*}^-) + O\left( \sqrt{ \frac{\ln M}{K} } \right)
$$

<br>

The more models $M$ we choose from, the higher the chance of overfitting, but the effect grows only logarithmically. If $M$ is infinite (like continuous $\lambda$ tuning), we use VC dimension to measure complexity instead of counting models. 

Now, let us summarize the data contamination we have discussed so far. As we saw earlier, the out-of-sample error is affected by optimistic bias, which introduces contamination. Beyond that, let’s consider the three data sets we used to estimate different types of error: 

<br>

$$
\boldsymbol{E}_{\text{in}},\quad \boldsymbol{E}_{\text{test}},\quad \boldsymbol{E}_{\text{val}}
$$

<br>

First, the training set, used to compute the in-sample error, is completely contaminated because it was directly involved in the learning process.

Second, the test set, used to estimate the test error, is totally clean, since it was not involved in training or any decision-making.

Lastly, the validation set, used to estimate the validation error, is slightly contaminated, as it was used both to approximate the out-of-sample error and to help decide where to stop training. To summarize, 

<br>

<div align="center">

<b>Training set</b>: totally contaminated <br>
<b>Validation set</b>: slightly contaminated <br> 
<b>Test set</b>: totally 'clean' 

</div>

<br>

We should have not only one validation set. We could have a number of them, such that when one of them gets contaminated, we move on to the other one which has not been used for decisions, and therefore the estimates will be reliable. Now we go to cross-validation.

---

#### 3. Cross Validation 

Let us start with the dilemma about $K$. We have the following chain of reasoning: 

<br>

$$
E_{\text{out}}(g) \approx E_{\text{out}}(g^{-}) \approx E_{\text{val}}(g^{-})
$$

<br>

To satisfy the first and second term, $K$ should be small. In contrast, to satisfy the second and thrid term, $K$ should be large. This is our dilemma. Can we have $K$ both small and large? To solve this dilemma, we introduce Leave One Out method. 

Consider we are given $N-1$ points for training and $1$ point for validation. We call this training set $\mathcal{D}_n$. And let us call the final hypothesis set learned from $\mathcal{D}_n$ as $g_n^-$. Since we excluded only $1$ point, it will be close to $g$. 

Now, let us estimate the $E_{\text{val}}(g_n^-)$. Sice we choose only 1 point for validation set: 

<br>

$$
\mathbf{e}_n = E_{\text{val}}(g_n^{-}) = e\left(g_n^{-}(\mathbf{x}_n),\ y_n\right)
$$

<br>

However, $K$ is too small. So we are going to repeat this exercise for every $n$, and compute the average of them. It can be described as below: 

<br>

$$
E_{\text{cv}} = \frac{1}{N} \sum_{n=1}^{N} \mathbf{e}_n
$$

<br>

We call it Cross Validation Error. Now we solved the dilemma of $K$. To aid understanding, we describe cross-validation as below: 

![solution](/assets/images/val_6.svg) 

If we apply the leave-one-out method, we can obtain the following cross-validation error: 

<br>

$$
E_{\text{cv}} = \frac{1}{3} \left(\mathbf{e}_1 + \mathbf{e}_2+ \mathbf{e}_3 \right)
$$

<br>

Now, let us apply Cross Validation for model selection. We compare linear model, illustrated above figure, and constant model. Which one is better model? 

![solution](/assets/images/val_7.svg) 

Although the exact value of the cross-validation error is not given, it is easy to see that the constant model has a lower cross-validation error just by visual comparison. So, constant model will be choosen. 

However, using leave-one-out in practice can be difficult. When the dataset is large, computing the cross-validation error becomes too time-consuming. For this reason, instead of leaving out just one data point, we typically group several data points together.

![solution](/assets/images/val_8.svg) 

One commonly used method is 10-fold cross-validation. This approach divides the entire dataset into $10$ parts, performs validation $10$ times, and takes the average of the results. Although the gap between the out-of-sample errors of $g$ and $g^{-}$ may be larger compared to leave-one-out, this method is generally preferred due to its computational efficiency.
