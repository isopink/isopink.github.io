---
layout: single
title: "Lecture 2 : Is Learning Feasible?"
---

In this time, we will talk about the question: **"Is learning feasible?"**. Let's answer this quention through the following four parts: 

1. Probability to the Rescue

2. Connection to Learning

3. Connection to Real Learning

4. A Dilemma and a Solution

---

#### 1. Probability to the Rescue 

![solution](/assets/images/2_1.svg)

Let’s begin by considering a bin filled with red and green balls.
If we randomly draw one ball from the bin, let the probability that it’s red be μ.
But we don’t know how many red balls are in the bin, so the exact value of μ is unknown.

To estimate μ, we randomly draw N balls from the bin and define ν as the fraction of red balls among them.

Can we then estimate μ using ν?
As you may already know, when N becomes large, the sample frequency (ν) tends to approximate the true probability (μ).
This intuition is mathematically justified by Hoeffding’s Inequality.

<Hoeffding’s Inequality>

The left-hand side represents the probability that ν is significantly different from μ — a bad event.

The right-hand side gives an upper bound on this probability.
If we reduce the error tolerance ε, the bound increases.
If we increase the sample size N, the bound decreases.

So the more we sample, the less likely the bad event becomes.
This makes intuitive sense.

In simple terms, saying “μ ≈ ν” is a form of PAC (Probably Approximately Correct).

Hoeffding’s inequality holds for any ε and N.
But here's a key idea:
In reality, the true mean generates the sample average.
However, since we don’t know the true mean, we interpret the sample average as approximating the true mean, thanks to Hoeffding’s inequality.
