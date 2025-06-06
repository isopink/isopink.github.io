---
layout: single
title: Introduction to Linear algebra 
---


In this time, I will introduce the central problem of Linear Algebra: *Solving linear equations*. Let’s start with the simplest case. We have $n$ equations in $n$ unknowns, where $n = 2$ : 

<br>

$$
\begin{array}{rl}
\textbf{Two equations} & \quad 1x + 2y = 3 \\
\textbf{Two unknowns}  & \quad 4x + 5y = 6.
\end{array}
$$



<br>

There are two ways of finding $x$ and $y$ : *Elimination and Determinants.*

---

*1. Elimination.*  
Subtract 4 times the first equation from the second equation. It leaves one equation for $y$ :

<br>

$$
\textbf{(equation 2)} - 4\textbf{(equation 1)} \quad \text{gives} \quad -3y = -6
$$

<br>

Immediately we know $y = 2$.  
Then $x$ comes from the first equation $1x + 2y = 3$:

<br>

$$
\textbf{Back-substitution} \quad 1x + 2(2) = 3 \quad \text{gives} \quad x = -1
$$

<br>

This process is essentially no different from *Gaussian Elimination*, which will be introduced soon.


---

*2. Determinants.*  
The solution $y = 2$ and $x = -1$ depends completely on the six coefficients. There must be a formula for $x$ and $y$. It is a *ratio of determinants* (or *Cramer's Rule*). It may seem mysterious unless you already know about 2x2 determinants — I will explain it later!

<br>

$$
x =
\frac{
\left|
\begin{array}{cc}
3 & 2 \\
6 & 5 \\
\end{array}
\right|
}{
\left|
\begin{array}{cc}
1 & 2 \\
4 & 5 \\
\end{array}
\right|
}
= \frac{3 \cdot 5 - 2 \cdot 6}{1 \cdot 5 - 2 \cdot 4}
= \frac{3}{-3} = -1
$$

<br>

$$
y =
\frac{
\left|
\begin{array}{cc}
1 & 3 \\
4 & 6 \\
\end{array}
\right|
}{
\left|
\begin{array}{cc}
1 & 2 \\
4 & 5 \\
\end{array}
\right|
}
= \frac{1 \cdot 6 - 3 \cdot 4}{1 \cdot 5 - 2 \cdot 4}
= \frac{-6}{-3} = 2
$$

<br>


These two approaches provide exactly same result. However, if $n$ is sufficiently large, solving linear systems by *Cramer's rule* becomes a computational Challenge. Instead, it is better to use *Gaussian Elimination.* This is the algorithm that is constantly used to slove large linear systems, and what we will see in the first Chapter. it's gonna be the basis for half of Linear algebra. Furthermore, During the first Chapter, I want to explain four deeper aspects : 

1. Linear eqautions lead to geomerty of planes. 

2. Matrix notations

3. Singular case. 

4. Rough count of the number of elimination steps. 

Now let's begin.

> **Reference**  
> Gilbert Strang, *Linear Algebra and Its Applications*, 4th Edition  
> MIT OpenCourseWare (MOOC)
