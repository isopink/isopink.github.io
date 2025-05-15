---
layout: single
title: Geometry of Linear Algebra
---

In this time, I will introduce the *geometry of linear equations*. This part changed how I view linear euqations entirely. To reduce cognitive load, let's begin with an extremely simple linear system. 

<br>

$$
\begin{aligned}
2x - y &= 1 \\
x + y &= 5
\end{aligned}
$$

<br>

We can look at this system *by rows* and *by columns*. We will check both of them. 

---


*1. By rows.*  
Draw a line of two equations($rows$) on the $x-y$ plane. There is a point of intersection lies on both lines. It is the point $x=2$ and $y=3$. This is the only soution to both equations($rows$). 

![교점 그래프](/assets/images/Figure_1.png)

I think you may have already noticed. This is exactly the same method that we learned in high school to solve linear equations.


---


*2. By columns.*  

<br>

$$
\textbf{Column form} \quad
x \begin{bmatrix} 2 \\ 1 \end{bmatrix}
+ y \begin{bmatrix} -1 \\ 1 \end{bmatrix}
= \begin{bmatrix} 1 \\ 5 \end{bmatrix}.
$$
<br>
