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

(*Here is a short proof*) The left-hand side represents the probability that $ν$ is significantly different from $μ$ — *the bad event.* The right-hand side gives an upper bound on this probability. If we reduce the error tolerance $ε$, the bound increases. If we increase the sample size $N$, the bound decreases. We can accept this intuitively.


Here is a key idea: In reality, population mean generates the sample mean. However, since we don’t know the population mean, we interpret the sample mean as approximating the population mean, thanks to Hoeffding’s inequality. In other words, saying $μ ≈ ν$ is **Probably Approximately Correct**.


---

#### 2. Connection to Learning

How does this bin model relate to learning? At first, the only unknown was a number $μ$, but in learning, we’re dealing with an unknown function $𝑓 : 𝑋 → 𝑌$. Still, the two cases are connected. Let’s choose a hypothesis $ℎ ∈𝐻$. 

For each input $𝑥 ∈ 𝑋$, if $h(x)=f(x)$, mark it green; otherwise, mark it red. Since we don’t know $f$, we don’t know the actual colors. However, if we pick $x$ randomly based on a probability distribution $P$ then the probability that $h(x) \ne f(x)$ (a red marbles) is some value $μ$. This turns the input space $X$ into a probabilistic bin. 

![solution](/assets/images/2_2.svg)

Training data points are like marbless drawn from the bin
Each point is independently drawn from $P$ and labeled red*(incorrect)* or green*(correct)* depending on whether $h(x_n)$ matches $f(x_n)$. **Thus, the learning problem becomes a probabilistic bin model, even if $P$ or $μ$ is unknown.** What $\mu$ tells us is the error rate $h$ makes in approximating $f$. If $\nu$ happens to be close to zero, we can predict that $h$ will approximate $f$ well over the entire input space. Now, we can update the learning diagram we introduced previously:

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

![solution](/assets/images/2_6.svg) 

Let's flip a coin (if you have). The probability of getting $10$ heads in a row with one coin is about $0.1%$. But if you flip $1,000$ coins, the chance that at least one shows $10$ heads in a row is about $0.63$. This shows that if you have many hypotheses, one of them may look good just by chance — even if it’s actually bad. We need to fix the bound. 

Let $g = \argmax_{h_i} \left( E_{in}(h_i) \right)&. The way to get around this is to try to bound 
$\mathbb{P}\left[ |E_{in}(g) - E_{out}(g)| > \epsilon \right]$ in a way that does not depend on which $g$ the learning algorithm picks. There is a simple but crude way of doing that. Since $g$ has to be one of the $h_m$’s regardless of the algorithm and the sample, it is always true that:

<br>

$$
\begin{aligned}
|E_{in}(g) - E_{out}(g)| > \epsilon &\Longrightarrow\ |E_{in}(h_1) - E_{out}(h_1)| > \epsilon \\[1em]
&\mathbf{or} \quad \, |E_{in}(h_2) - E_{out}(h_2)| > \epsilon \\[1em]
&\quad \vdots \\[1em]
&\mathbf{or} \quad \, |E_{in}(h_M) - E_{out}(h_M)| > \epsilon
\end{aligned}
$$

<br>

$B_1 \Rightarrow B_2$ means that event $B_1$ implies event $B_2$. Although the events on the right-hand-side cover a lot more than the left-hand-side, the right-hand-side has the property we want; the hypotheses $h_m$ are fixed. We now apply two basic rules in probability: 

<br>

$$
\text{if } B_1 \Rightarrow B_2, \text{ then } \mathbb{P}[B_1] \leq \mathbb{P}[B_2]
$$

<br>

And, if $B_1, B_2, \cdots, B_M$ are any events, then:

<br>

$$
\mathbb{P}[B_1 \text{ or } B_2 \text{ or } \cdots \text{ or } B_M] \leq \mathbb{P}[B_1] + \mathbb{P}[B_2] + \cdots + \mathbb{P}[B_M]
$$

<br>

The second rule is known as the *union bound*. Putting the two rules together, we get: 

<br>

$$
\mathbb{P}\left[ \left| E_{\text{in}}(g) - E_{\text{out}}(g) \right| > \epsilon \right]
\leq
\sum_{m=1}^{M} \mathbb{P} \left[ \left| E_{\text{in}}(h_m) - E_{\text{out}}(h_m) \right| > \epsilon \right]
$$

<br>

Then, apply the Hoeffding Inequality to the *M* terms one at a time, we meet the final form: 

<br>

$$
\mathbb{P}\left[ \left| E_{\text{in}}(g) - E_{\text{out}}(g) \right| > \epsilon \right] \leq 2M e^{-2\epsilon^2 N}.
$$

<br>

It was a long journey. We are trying to simultaneously approximate all $E_{\text{out}}(h_m)$’s by the corresponding $E_{\text{in}}(h_m)$’s. This allows the learning algorithm to choose any hypothesis based on $E_{\text{in}}$ and expect that the corresponding $E_{\text{out}}$ will uniformly follow suit, regardless of which hypothesis is chosen.  

---

This inequality is only meaningful if $M$ is finite. Unfortunately, in general problems, the number of hypotheses is very large. **To make this inequality meaningful, we need to make $M$ tighter.** Stay curious — we will look into this soon.


