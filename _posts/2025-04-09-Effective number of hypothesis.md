---
layout: single
title: "Lecture 5 : Effective number of hypothesis"
---


In this time, we will talk about how to reduce the number of hypothesis, $M$ which we discussed in [<u>Lecture 2</u>.](https://isopink.github.io/Is-Learning-Feasible/)  The discussion will proceed in the following three parts :


1. Where did the $M$ come from? 

2. Ilustrative examples 

3. Break point 

---

#### 1. Where did the $M$ come from? 

At the end of the sesiion, I promised to make $M$ tighter. This is the right time to do that 

<br>

$$
\mathbb{P}\left[ \lvert E_{\text{in}} - E_{\text{out}} \rvert > \epsilon \right] \leq 2M e^{-2\epsilon^2 N}
$$

<br>

This is the inequality we discussed in Lecture 2. The problem is $M$ is almost infinity in most cases, the inequality becomes useless. Before findnig good replacement of $M$, See where dose $M$ come from. 

In Hoeffding’s Inequality, the probability $\mathbb{P}$ refers to the **bad event**. This bad event is defined as the case where the difference between the in-sample error and out-of-sample error exceeds $\epsilon$ for a given hypothesis. Now, because we want this guarantee to hold **for all $M$ possible hypotheses**, we had to consider the worst-case scenario —  that is, assume that **each bad event is mutually exclusive**. 

Under this assumption, we simply added the individual probabilities of each bad event, which is how the factor $M$ ended up in the inequality. **But, in real, These hypotheses might not be mutually exclusive.** The bad events are very overlapping.  


