---
layout: single
title: "Lecture 1 : The Learning Problem" 
---

In this time, I will introduce the concept of the learning problem in the context of machine learning. The discussion will proceed in the following five parts : 
<br>

1. Example of machine learning   

2. Components of a Learning   

3. A simple model   

4. Types of learning   

5. Puzzle


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

$$
\mathbf{x} = (\text{Age}, \text{Gender}, \text{Income}, \ldots)
$$

The output $y$ denotes the decision:

$$
y = \begin{cases}
+1 & \text{(Approved)} \\
-1 & \text{(Rejected)}
\end{cases}
$$

We assume the existence of an ideal function $$ f : \mathbb{R}^d \rightarrow \{-1, +1\}, $$ which perfectly maps inputs $\mathbf{x}$ to outputs $y$. We refer to this unknown function as the **Target Function**. Since the target function $f$ is unknown, our goal is to find an approximation $g$ — a **Hypothesis** — that best captures the behavior of $f$, based on observed data.



> **Reference**  
> Yaser S. Abu-Mostafa, *Learning from data*, AMLBook, 2012    
> Caltech Edu(MOOC)
