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

<div align="center">

| Attribute            | Value       |
|----------------------|-------------|
| age                  | 23 years    |
| gender               | male        |
| annual salary        | $30,000     |
| years in residence   | 1 year      |
| years in job         | 1 year      |
| current debt         | $15,000     |
| ...                  | ...         |

</div>

You have to decide whether to approve or rejecte these applications. To automate this task, we consider learning from historical application records. Let us now formalize the problem more mathematically.

<div align="center">

| Item           | Symbol / Definition             | Meaning                                |
|:--------------:|:-------------------------------:|:--------------------------------------:|
| Input          | **x**                           | Customer application                   |
| Output         | *y*                              | Good or bad customer?                  |
| Target function| *f : 𝓧 → 𝓨*                      | Ideal credit approval formula          |
| Data           | *(x₁, y₁), … , (xₙ, yₙ)*         | Historical records                     |
| Hypothesis     | *g : 𝓧 → 𝓨*                      | Formula to be used (learned model)     |

</div>
> **Reference**  
> Yaser S. Abu-Mostafa, *Learning from data*, AMLBook, 2012    
> Caltech Edu(MOOC)
