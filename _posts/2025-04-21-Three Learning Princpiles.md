---
layout: single
title: "Lecture 17 : Three Learning Principles"
---

In this time, we introduce Three Learning Principles. These are related to the model selection and data handling. The discussion will proceed in the following three parts: 

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

<이미지1>

Despite its complex-looking decision boundary, it’s defined by a relatively small number of support vectors—so it belongs to a small class of hypotheses. Let us discuss one more funny puzzle about exceptions. 

Imagine receiving a letter each week predicting the outcome of a football game—win or lose. We follow the predictions, and week after week, they are always correct. After five weeks of perfect predictions, the sender asks us to pay $50 to keep receiving them. Should we trust them?

<이미지2>

This puzzle presents that exact scenario. On the figure above, we see sequences of $0$s and $1$s. Each of them represent a set of weekly predictions. Each row corresponds to a different person receiving the predictions. The $0$ or $1$ at the end shows whether the person’s predictions were correct over the five weeks.

Among these people, some just happen to get all the predictions right. For example, the person with arrow received five correct predictions in a row. It looks impressive, but the trick is that there are many different people receiving different prediction letters. With enough people, it’s statistically likely that someone will get five correct predictions just by chance.

This illustrates a key idea. Even if a model performs perfectly on training data, that doesn’t mean it’s genuinely good—it could just be overfitting. The oracle’s perfect record is not necessarily meaningful if we don’t know how many people were sent different letters. Random success is not the same as true predictive power.
