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


1. *By rows.*  
Draw a line of two equations($rows$) on the $x-y$ plane. There is a point of intersection lies on both lines. It is the point $x=2$ and $y=3$. This is the only soution to both equations($rows$). 

![intersection](/assets/images/Figure_1.png)

I think you may have already noticed. This is exactly the same method that we learned in high school to solve linear equations.


---


2. *By columns.*   
Look at the *columns* of the linear system. The two separate equations are really *one vector equation*:


<br>

$$
\textbf{Column form} \quad
x \begin{bmatrix} 2 \\ 1 \end{bmatrix}
+ y \begin{bmatrix} -1 \\ 1 \end{bmatrix}
= \begin{bmatrix} 1 \\ 5 \end{bmatrix}.
$$

<br>

The problem is to find the combination of the *column vectors* on the left side that produces the vector on the right side. Those column vectors $(2,1)$ and $(-1,1) $ are represented by red and blue lines below. The unknowns are the numbers $x$ and $y$ that multiply the column vectors. 

![combination](/assets/images/Figure_2.png)

The whole idea can be seen in that figure, where $2$ times (column 1) is added to $3$ times (column 2). Geometrically, this produces a famous parallelogram. Algebrically, it produces the correct vector $(1,5)$, the right side of our *column form*. It confirms that $x=2$ and $y=3$. Surprisingly, the result is same when we look at the linear system "*by rows*". So far, the system has been simple. Now, let’s extend it to three equations with three unknowns.

---

