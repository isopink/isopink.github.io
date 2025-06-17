---
layout: single
title: "Lecture 17 : Three Learning Principles"
---

This is the end of our journey with Learning from data. This time, we introduce Three Learning Principles. These are related to the model selection and data handling. The discussion will proceed in the following three parts: 

1. Occam's Razor

2. Sampling Bias

3. Data Snooping

--- 

#### 1. Occam's Razor 

According to Occam's Razor, the simplest model that adequately explains the data is usually the most plausible. We have two questions about the idea. First, what does it mean for a model to be simple? Second, How do we know that simple is better? We will answer these questions one by one.

<br>

##### 1.1. Meanning of 'simple' 

But what exactly does simple mean in machine learning? To understand this, we need to explore the concept of complexity. There are two kinds of complexity to consider: the complexity of a single hypothesis $h$, and the complexity of the hypothesis set $\mathcal{H}$.

The complexity of $h$ refers to how complicated an individual model is—for example, the degree of a polynomial or its description length (MDL). This matches our everyday intuition of what makes a model simple. In contrast, the complexity of $\mathcal{H}$ captures how rich or flexible the entire set of models is, measured by things like entropy or [VC dimension](https://isopink.github.io/VC-Dimension/).

While we usually think of simplicity in terms of $h$, theoretical proofs about learning use the complexity of $\mathcal{H}$. So, there’s a gap between our intuition and the math, and understanding both is key. We now connect $h$ and $\mathcal{H}$. 

Suppose it takes $\ell$ bits to describe a hypothesis $h$. That means $h$ is one of $2^\ell$ possible hypotheses. In other words, if we can describe $h$ using a small number of bits, then the set $\mathcal{H}$ that contains all such possible $h$'s is also relatively small. So, a simpler $h$ (low-bit description) implies a smaller or less complex $\mathcal{H}$, and vice versa.

What if $h$ has real-valued parameters, like in a high-order polynomial? For example, a 17th-order polynomial may appear as just one function, but it has many degrees of freedom—making it complex and one of many in a large hypothesis set.

However, there are exceptions. Some models may look complex in form but actually come from a small hypothesis set. A good example is the [Support Vector Machine](https://isopink.github.io/SVM/).


![image1](./image1.png)

Despite its complex-looking decision boundary, it’s defined by a relatively small number of support vectors—so it belongs to a small class of hypotheses. Let us discuss one more funny puzzle about exceptions. 

Imagine receiving a letter each week predicting the outcome of a football game—win or lose. We follow the predictions, and week after week, they are always correct. After five weeks of perfect predictions, the sender asks us to pay 50 dollars to keep receiving them. Should we trust them?


![image1](./image1.png)


This puzzle presents that exact scenario. On the figure above, we see sequences of $0$s and $1$s. Each of them represent a set of weekly predictions. Each row corresponds to a different person receiving the predictions. The $0$ or $1$ at the end shows whether the person’s predictions were correct over the five weeks.

Among these people, some just happen to get all the predictions right. For example, the person with arrow received five correct predictions in a row. It looks impressive, but the trick is that there are many different people receiving different prediction letters. With enough people, it’s statistically likely that someone will get five correct predictions just by chance.

This illustrates a key idea. Even if a model performs perfectly on training data, that doesn’t mean it’s genuinely good—it could just be overfitting. The oracle’s perfect record is not necessarily meaningful if we don’t know how many people were sent different letters. Random success is not the same as true predictive power. 

<br>

##### 1.2. Why is simpler better? 

A simpler model is considered better not because it is more elegant or aesthetically pleasing, but because it tends to perform better on unseen data. In other words, it has better out-of-sample performance. 

This advantage comes from the fact that simpler models have fewer hypotheses in their hypothesis set, which we denote as:

<br>

$$
m_{\mathcal{H}}(N) \text{for a dataset of size} \, N
$$

<br> 

This is the growth function, typically used for binary classification, discussed in [Lecture 5](https://isopink.github.io/Effective-number-of-hypothesis/). Since they can represent fewer possible mappings from input to output, simpler models are less likely to fit a training dataset purely by chance. The probability of such a coincidental fit is approximately:

<br>

$$
m_{\mathcal{H}}(N)
$$

<br>

where $2^N$ is the total number of possible binary labelings of the dataset. A lower value of $m_{\mathcal{H}}(N)$ implies a lower risk of overfitting. In contrast, a more complex model typically has a much larger hypothesis set and can match many different labelings of the data. This flexibility increases the chance of finding a hypothesis that fits the training data well — even if that fit captures noise rather than real structure. In such cases, the model may appear to perform well during training but fail to generalize to new examples. 

This leads us to previous puzzle in (1.1). One of those letters will inevitably be correct. To that one recipient, the scammer looks like a genius. But the prediction was not meaningful. It was just one out of many guesses. A model with a hypothesis set as large as $2^N$ is doing the same thing. It’s making all possible guesses, and one of them will fit the data, but we can't trust it. In contrast, a simple model with only one possible hypothesis $m_{\mathcal{H}}(N) = 1$ can’t cheat like that. If it fits the data, we have reason to believe it discovered something real.

In conclusion, when a simple model achieves a good fit, it is statistically more meaningful. It suggests that the model is capturing a genuine pattern in the data, rather than memorizing it. This is why simplicity is favored in learning theory, not for its elegance, but because it leads to more reliable and generalizable predictions.

However, a good fit is only meaningful if it is falsifiable. A model that always fits the data, either because it's too flexible or the dataset is too limited, offers no real evidence. Let us look at clear exmaple, where two scientists test whether conductivity is linear in temperature. 

![image1](./image1.png)

Scientist A uses only two points, which always form a line, while Scientist B uses three. Only B's experiment is falsifiable since the third point had deviated, the model would have been clearly wrong. The key point is that a fit that cannot fail tells us nothing. Falsifiability gives meaning to a model's success. When combined with simplicity, it leads to models that are not just statistically sound, but also scientifically meaningful. 

---

#### 2. Sampling Bias 

Let us begin with the puzzle about Presidential election. In 1948, Harry Truman and Thomas Dewey faced off in one of the most famously mispredicted presidential elections in U.S. history. A major newspaper at the time conducted a phone poll to gauge public opinion and found that Dewey was leading by a large margin. Confident in the poll results, the newspaper prematurely printed the headline, “DEWEY DEFEATS TRUMAN.” However, the actual election result turned out quite differently. Truman won. What went wrong? 

![image1](./image1.png)

The problem wasn’t the size of the poll, but how the data was collected. In 1948, phones were not yet widespread and were mostly owned by wealthier individuals. As a result, the sample used in the poll was not representative of the overall voting population. This is a classic case of sampling bias. The process used to gather data introduced a systematic error, leading to a faulty prediction.

From a machine learning perspective, this example highlights an essential lesson: having more data is not enough if the data isn’t representative. Even the best models can produce misleading results when trained on biased or poorly collected datasets. Ultimately, the quality and representativeness of data matter more than quantity when it comes to making reliable predictions.
