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

The complexity of $h$ refers to how complicated an individual model is—for example, the degree of a polynomial or its description length (MDL). This matches our everyday intuition of what makes a model simple. In contrast, the complexity of $\mathcal{H}$ captures how rich or flexible the entire set of models is, measured by things like entropy or VC dimension.

While we usually think of simplicity in terms of $h$, theoretical proofs about learning use the complexity of $\mathcal{H}$. So, there’s a gap between our intuition and the math, and understanding both is key. We now connect $h$ and $\mathcal{H}$. 

Suppose it takes $\ell$ bits to describe a hypothesis $h$. That means $h$ is one of $2^\ell$ possible hypotheses. In other words, if we can describe $h$ using a small number of bits, then the set $\mathcal{H}$ that contains all such possible $h$'s is also relatively small. So, a simpler $h$ (low-bit description) implies a smaller or less complex $\mathcal{H}$, and vice versa.

What if $h$ has real-valued parameters, like in a high-order polynomial? For example, a 17th-order polynomial may appear as just one function, but it has many degrees of freedom—making it complex and one of many in a large hypothesis set.

