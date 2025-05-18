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

This is the error rate wthin the sample, which corresponds to $ν$ in the bin model. It will be called the *in-sample error*. If the [statement] is true, returns $1$, otherwise, returns $0$. In the same way, we define the *out-of-sample error* below:

<br>

$$
E_{out}(h) = \mathbb{P}[h(\mathbf{x}) \ne f(\mathbf{x})]
$$

<br>

It corresponds to $μ$ in the bin model. The probability is based on the distribution *P* over *X* which is used to sample the data points *x*. We can now rewrite Hoeffding's Inequality using $E_{in}$ and $E_{out}$: 

<br>

$$
\mathbb{P}\left[\,|E_{in}(h) - E_{out}(h)| > \epsilon\,\right] \leq 2e^{-2\epsilon^2 N} \quad \text{for any } \epsilon > 0
$$

<br>

---

#### 4. A dilemma and a solution. 

![solution](/assets/images/2_5.svg) 

It seems we have solved the problem. By using Hoeffding's inequality, we can estimate the $μ$ from $ν$ and by introducing multiple bins, we have extended the number of hypotheses in a finite way. Are we done? Unfortunately, not yet! **Hoeffing doesn't apply to multiple bins.** We need to know the reason, intuitively. 

![solution](/assets/images/2_5.svg) 

Let's flip a coin (if you have). The probability of getting $10$ heads in a row with one coin is about $0.1%$. But if you flip $1,000$ coins, the chance that at least one shows $10$ heads in a row is about $63%$. This shows that if you have many hypotheses, one of them may look good just by chance — even if it’s actually bad.


The way to get around this is to try to bound $\mathbb{P}[|E_{in}(g) - E_{out}(g)| > \epsilon]$ in a way that does not depend on which $g$ the learning algorithm picks. There is a simple but crude way of doing that. Since $g$ has to be one of the $h_m$'s regardless of the algorithm and the sample, it is always true that

<br>

$$
\begin{aligned}
|E_{in}(g) - E_{out}(g)| > \epsilon &\Longrightarrow\ |E_{in}(h_1) - E_{out}(h_1)| > \epsilon \\[1em]
&\mathbf{or} \quad \, |E_{in}(h_2) - E_{out}(h_2)| > \epsilon \\[1em]
&\quad \vdots \\[1em]
&\mathbf{or} \quad \, |E_{in}(h_M) - E_{out}(h_M)| > \epsilon
\end{aligned}
$$
