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

Here is how it works. You describe a movie as a long array of different factors, e.g., Now, you describe each viewer with corresponding factors; how much do they like comedy, do they prefer simple or complicated plots, how important are the looks of the lead actor, and so on. How this viewer will rate that movie is now estimated based on the match/mismatch of these factors. For example, if the movie is pure comedy and the viewer hates comedies, the chances are he won’t like it. If you take dozens of these factors describing many facets of a movie’s content and a viewer’s taste, the conclusion based on matching all the factors will be a good predictor of how the viewer will rate the movie. This solution represents a straightforward mapping between viewer and movies, but it is not powered by machine learning.

![solution](/assets/images/fig_2.svg)

**The power of machine learning lies in its ability to automate whole matching processes.** All you need is previous rating redords, *The data*. It starts with random factors, then tunes these factors to make them more and more aligned with how viewers have rated movies before, until they are ultimately able to predict how viewers rate movies in general. The factors we end up with may not be as intuitive as ‘comedy content’, and in fact can be quite subtle or even incomprehensible. After all, the algorithm is only trying to find the best way to predict how a viewer would rate a movie, not necessarily explain to us how it is done. This algorithm was part of the winning solution in the million-dollar competition. 

To do so, the following three conditions must be satisfied: 


(a) A pattern exists.   
(b) We cannot pin it down mathematically.    
(c) **We have data on it**    


