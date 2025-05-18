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


Can we estimate $μ$ using $ν$? As you may already know, when $N$ becomes large, the sample frequency $ν$ tends to approximate the true probability $μ$.
This intuition is mathematically justified by **Hoeffding’s Inequality**. 

<br>

$$
\mathbb{P}(|\nu - \mu| > \epsilon) \leq 2e^{-2\epsilon^2 N} \quad \text{for any } \epsilon > 0.
$$

<br>

(*Here is a short proof*) The left-hand side represents the probability that $ν$ is significantly different from $μ$ — *the bad event.* The right-hand side gives an upper bound on this probability. If we reduce the error tolerance $ε$, the bound increases. If we increase the sample size $N$, the bound decreases. We can accept this intuitively. In other words, saying $μ ≈ ν$ is **Probably Approximately Correct**.


Here is a key idea: In reality, population mean generates the sample mean. However, since we don’t know the population mean, we interpret the sample mean as approximating the population mean, thanks to Hoeffding’s inequality.


---

#### 2. Connection to Learning

How does this bin model relate to learning? At first, the only unknown was a number $μ$, but in learning, we’re dealing with an unknown function $𝑓 : 𝑋 → 𝑌$. Still, the two cases are connected. Let’s choose a hypothesis $ℎ ∈𝐻$. 

For each input $𝑥 ∈ 𝑋$, if $h(x)=f(x)$, mark it green; otherwise, mark it red. Since we don’t know $f$, we don’t know the actual colors. However, if we pick $x$ randomly based on a probability distribution $P$ then the probability that $h(x) \ne f(x)$ (a red marbles) is some value $μ$. This turns the input space $X$ into a probabilistic bin. 

![solution](/assets/images/2_2.svg)

Training data points are like marbless drawn from the bin
Each point is independently drawn from $P$ and labeled red*(incorrect)* or green*(correct)* depending on whether $h(x_n)$ matches $f(x_n)$. **Thus, the learning problem becomes a probabilistic bin model, even if $P$ or $μ$ is unknown.** Now, we can update the learning diagram we introduced previously:

![solution](/assets/images/2_3.svg) 

---

#### 3. Connection to REAL learning

Are we done now? Unfortunately, no. Using a single hypothesis is not learning — **it’s verification**.

In real learning, we want to choose the best hypothesis from a set of hypotheses $H$. This means we must deal with multiple hypotheses, not just one. Our situation is illustrated in the following figure: 

![solution](/assets/images/2_4.svg) 
  
To analyze this more clearly, we introduce new terms: 

<br>

$$
\begin{aligned}
E_{in}(h) 
&= \text{(fraction of } \mathcal{D} \text{ where } f \text{ and } h \text{ disagree)} \\[1em]
&= \frac{1}{N} \sum_{n=1}^{N} [h(x_n) \ne f(x_n)]
\end{aligned}
$$

<br>

<br>


