---
layout: single
title: "Lecture 1 : The Learning Problem" 
---

In this time, I will introduce the concept of the learning problem in the context of machine learning. The discussion will proceed in the following four parts : 
<br>

1. Example of machine learning   

2. Components of a Learning   

3. A simple model   

4. Types of Learning   


---


#### 1. Example of machine learning.

Netflix recommends movies to user. To improve the accuracy of its recommendations, Netflix hosted a million-dollar competition. One such solution is illustrated below: 

![solution](/assets/images/fig_1.svg)

Here is how it works. You describe a movie as a long array of different factors, e.g., Now, you describe each viewer with corresponding factors; how much do they like comedy, do they prefer simple or complicated plots, how important are the looks of the lead actor, and so on. How this viewer will rate that movie is now estimated based on the match/mismatch of these factors. This solution represents a straightforward mapping between viewer and movies, but it is not powered by machine learning.

![solution](/assets/images/fig_2.svg)

**The power of machine learning lies in its ability to automate whole matching processes.** All you need is previous rating redords, *The data*. It starts with random factors, then tunes these factors to make them more and more aligned with how viewers have rated movies before, until they are ultimately able to predict how viewers rate movies in general. The algorithm is only trying to find the best way to predict how a viewer would rate a movie. This was part of the winning solution in the million-dollar competition. 

To do so, the following three conditions must be satisfied: 


(a) A pattern exists.     
If no underlying pattern exists in the data, then learning is not possible. 

   
(b) We cannot pin it down mathematically.    
If a problem can be fully described with mathematical rules, there is no need to this.

   
(c) We have data on it   
Machine learning fundamentally relies on historical data to predict future outcomes. 
This is the motivation behind the title of the well-known textbook, **Learning from Data** 

---


#### 2. Components of Learning.
Let us now consider a different example. Suppose you are working at a financial institution that receives thousands of credit card applications every day. Here is an example of applicant information.
<br>


| Attribute            | Value       |
|----------------------|-------------|
| age                  | 23 years    |
| gender               | male        |
| annual salary        | $30,000     |
| years in residence   | 1 year      |
| years in job         | 1 year      |
| current debt         | $15,000     |
| ...                  | ...         |


<br>
You have to decide whether to approve or rejecte these applications. To automate this task, we consider learning from historical application records. Let us now formalize the problem more mathematically.   

<br>


|  Item              | Symbol                                  | Meaning                    |
|-------------------|---------------------------------------------|--------------------------------------|
| Input             | *x*                                       | customer application              |
| Output            | *y*                                         | good/bad customer?                |
| Target function   | *f : 𝓧 → 𝓨*                                 | ideal credit approval formula     |
| Data              | *(x₁, y₁), ⋯, (xₙ, yₙ)*             | historical records                |
| Hypothesis        | *g : 𝓧 → 𝓨*                                 | formula to be used                |


<br>

The input vector $\mathbf{x} \in \mathbb{R}^d$ represents an applicant's features: 

<br>

$$\mathbf{x} = (\text{Age}, \text{Gender}, \text{Income}, \ldots)$$

<br>

The output $y$ denotes the decision you make.

<br>

$$
y = \begin{cases}
+1 & \text{(Approved)} \\
-1 & \text{(Rejected)}
\end{cases}
$$

<br>

We assume the existence of an ideal function $ f : \mathbb{R}^d \rightarrow \{-1, +1\}, $ which perfectly maps inputs $x$ to outputs $y$. We refer to this unknown function as the **Target Function**. Since the target function $f$ is unknown, our goal is to find an approximation $g$ — a **Hypothesis** — that best captures the behavior of $f$, based on **Training Examples** and **Learning Algoritm**. We define the **Learning Model** as the combination of the Hypothesis Set and the Learning Algorithm. This whole process can be visualized as follows: 


![solution](/assets/images/fig_3.svg)

---

#### 3. A simple model   
As a concrete example of a learning model, we now introduce the **Perceptron**. It is a foundational linear classifier. It predicts binary labels by computing the sign of the inner product between a input vector and a weight vector. Let's see how it works.

<br>

$$
\begin{aligned}
\text{Approve credit if} \quad & \sum_{i=1}^{d} w_i x_i > \text{threshold}, \\
\text{Deny credit if} \quad & \sum_{i=1}^{d} w_i x_i < \text{threshold}.
\end{aligned}
$$

<br>

This formula can be written more compactly as
<br>

$$h(\mathbf{x}) = \text{sign} \left( \left( \sum_{i=1}^{d} w_i x_i \right) + b \right)$$

<br>

where $x_1, \cdots, x_d$ are the components of the vector $\mathbf{x}$. $h(\mathbf{x}) = +1$ means "approve credit" and $h(\mathbf{x}) = -1$ means "deny credit". $\text{sign}(s) = +1$ if $s > 0$, and $\text{sign}(s) = -1$ if $s < 0$. The weights are $w_1, \cdots, w_d$, and the threshold is determined by the bias term $b$, since credit is approved if:

<br>

$$
\sum_{i=1}^{d} w_i x_i > -b.
$$

<br>

Following Figure illustrates what a perceptron does in a two-dimensional case ($d = 2$). The plane is split by a line into two regions, the $+1$ decision region and the $-1$ decision region. Different values for the parameters $w_1, w_2, b$ correspond to different lines defined by the equation $w_1 x_1 + w_2 x_2 + b = 0$. If the data set is *linearly separable*, there will be a choice for these parameters that classifies all the training examples correctly.

![solution](/assets/images/fig_4.svg)

Some data points are misclassified. It indicates that the weight vector has not been properly set, which means our hypothesis $h \in H$ is not close enough to the target funtion *f*. To address this issue, we now introduce the **Perceptron Learning Algorithm (PLA)**. Before doing so, let us first simplify the perceptron formula.


To simplify the notation of the perceptron formula, we will treat the bias $b$ as a weight $w_0 = b$ and merge it with the other weights into one vector $\mathbf{w} = [w_0, w_1, \cdots, w_d]^\top$. We also treat $\mathbf{x}$ as a column vector and modify it to become $\mathbf{x} = [x_0, x_1, \cdots, x_d]^\top$, where the added coordinate $x_0$ is fixed at $x_0 = 1$. Formally speaking, the input space is now

<br>

$$
\mathcal{X} = \{1\} \times \mathbb{R}^d = \{ [x_0, x_1, \cdots, x_d]^\top \mid x_0 = 1,\ x_1 \in \mathbb{R}, \cdots,\ x_d \in \mathbb{R} \}.
$$

<br>

With this convention, $\mathbf{w}^\top \mathbf{x} = \sum_{i=0}^{d} w_i x_i$, can be rewritten in vector form as 

<br>

$$
h(\mathbf{x}) = \text{sign}(\mathbf{w}^\top \mathbf{x}).
$$

<br>

We now introduce the *perceptron learning algorithm* (PLA). The algorithm will determine what $\mathbf{w}$ should be, based on the data. Let us assume that the data set is linearly separable, which means that there is a vector $\mathbf{w}$ that makes the correct decision $h(\mathbf{x}_n) = y_n$ on all the training examples: 

![solution](/assets/images/fig_5.svg)

Our learning algorithm will find this $\mathbf{w}$ using a simple iterative method. At iteration $t$, where $t = 0, 1, 2, \dots$, there is a current value of the weight vector, call it $\mathbf{w}(t)$. The algorithm picks an example from $(\mathbf{x}_1, y_1), \dots, (\mathbf{x}_N, y_N)$ that is currently misclassified, call it $(\mathbf{x}(t), y(t))$, and uses it to update $\mathbf{w}(t)$. Since the example is misclassified, we have $y(t) \ne \text{sign}(\mathbf{w}^\top(t)\mathbf{x}(t))$. The update rule is:

<br>

$$
\mathbf{w}(t + 1) = \mathbf{w}(t) + y(t)\mathbf{x}(t)
$$

<br>

This rule moves the boundary in the direction of classfying $(\mathbf{x}(t))$ correctly: 

![solution](/assets/images/fig_5.svg)

The algorithm continues with further iterations until there are no longer misclassified examples in the data set. Despite updating the weights using only one misclassified example at a time, the perceptron learning algorithm is guaranteed to converge to a correct solution, assuming the data is linearly separable.
It works regardless of which misclassified example is chosen or how the weights are initialized. 

---

#### 4. Types of Learning   

The premise of machine learning can be broadly stated as follows:


**Use observations to infer the underlying process that generated them**


This definition is intentionally broad, and it is difficult to encapsulate all learning problems within a single framework. As a result, different learning paradigms have emerged to handle different types of data, tasks, and assumptions. Let me introduce three major types. 

---

##### 4.1. Supervised Learning.    

![solution](/assets/images/fig_5.svg)

Think about a vending machine that recognizes coins. We see a bunch of coins represented as dots, based on two features, *mass* and *size*. Each coin is colored and clustered. This is our *training examples*, where the correct label is already known. 

![solution](/assets/images/fig_6.svg)

This represent the model has learned where to draw a *decision boundares* between the coin types. Now we can recognize the coins. To simplify, supervised learning is **Learn a function from labeled examples.**

---

##### 4.2. Unsupervised Learning.    

![solution](/assets/images/fig_7.svg)

Let's think about a vending machine again. We see a bunch of coins represented as dots, but not sure about what type of coin it is. That is why dots are not colored. Despite the correct label is unknown, we can still *cluster* the coins. 

![solution](/assets/images/fig_8.svg)

This represent the model has learned where to draw a *decision boundaries* between clusters. We cannot recogize the coins, at least we can regonize the *difference* of them. To simplify, unsupervised learning is **Discover structure or patterns in data without labels**.

---

##### 4.3. Reinforcement Learning.   

Let’s take a real-world example of reinforcement learning: *Why doesn’t a baby touch boiling water?*


Well, maybe the first time the baby does, it’s very painful — a strong negative reward.
That pain acts as a signal: *touching hot water leads to a bad outcome.*

Over time, the baby learns to avoid that action. There’s no teacher explicitly saying 'don’t do that,' just feedback from the environment. This is exactly how reinforcement learning works — by associating actions with good or bad outcomes through trial and error. To simplify, Reinforcement learning is **Learn a policy to maximize reward through interaction with the environment**. We will talk about it later, more precisely. 

---

Next time. We will discuss the feasibility of learnig: **Can we make reliable prediction outside the training data using only what we have seen?**

> **Reference**  
> Yaser S. Abu-Mostafa, *Learning from data*, AMLBook, 2012    
> Caltech Edu(MOOC)
