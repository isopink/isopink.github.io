---
layout: single
title: "Lecture 2 : Is Learning Feasible?"
---

In this time, we will talk about the feasibility of learning. The discussion will proceed in the following four parts: 

1. Probability to the Rescue

2. Connection to Learning

3. Connection to Real Learning

4. A Dilemma and a Solution

---

#### 1. Probability to the Rescue 

![solution](/assets/images/2_1.svg)

Let’s begin by considering a bin filled with red and green marbles. If we randomly draw one marble from the bin, let the probability that it is red be $μ$.
However, we don’t know how many red marbless are in the bin, so the exact value of $μ$ is **unknown**. To estimate $μ$, we randomly draw $N$ marbles from the bin and define $ν$ as the fraction of red marbles among them.


Can we then estimate μ using $ν$? As you may already know, when $N$ becomes large, the sample frequency $ν$ tends to approximate the true probability $μ$.
This intuition is mathematically justified by **Hoeffding’s Inequality**. 

<br>

$$
\mathbb{P}(|\nu - \mu| > \epsilon) \leq 2e^{-2\epsilon^2 N} \quad \text{for any } \epsilon > 0.
$$

<br>

The left-hand side represents the probability that $ν$ is significantly different from $μ$ — *the bad event.* The right-hand side gives an upper bound on this probability. If we reduce the error tolerance $ε$, the bound increases. If we increase the sample size $N$, the bound decreases. We can accept this intuitively. In other words, saying $μ ≈ ν$ is **Probably Approximately Correct**.

Hoeffding’s inequality holds for any ε and N.
But here's a key idea:
In reality, the true mean generates the sample average.
However, since we don’t know the true mean, we interpret the sample average as approximating the true mean, thanks to Hoeffding’s inequality.
