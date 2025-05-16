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

![intersection](/assets/images/Figure_1.png)

I think you may have already noticed. This is exactly the same method that we learned in high school to solve linear equations.


---


*2. By columns.*   
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

The whole idea can be seen in that figure, where $2$ times (column 1) is added to $3$ times (column 2). Geometrically, this produces a famous parallelogram. Algebrically, it produces the correct vector $(1,5)$, the right side of our *column form*. It confirms that $x=2$ and $y=3$. Surprisingly, the result is same when we look at the linear system "*By rows*". 

---
So far, the system has been simple. Now, let’s extend it to three equations with three unknowns: 

<br>

$$
\begin{aligned}
2u &+ v  &+ w   &= 5 \\
4u &- 6v   &    &= -2 \\
-2u &+ 7v &+ 2w &= 9
\end{aligned}
$$

<br>
Again, We can look at this system by rows and by columns. We will chekt it out again! 

---

*1. By rows.*   
Each equation describes a plane in three dimensions. The first plane is $2u+v+w=5$, and the second plane is $4u-6v=-2$. These two planes make intersection line. 

![intersection](/assets/images/Figure_3.png)

Finally, the third plane intersects the line in at $u=1$, $v=1$, $w=2$. This triple intersection point $(1,1,2)$ solves the linear system. 

![intersection](/assets/images/Figure_4.png)

---

*2. By columns.*  
As we checked earlier in the system with two equations and two unknowns, we are going to make one vector equation: 


<br>

$$ u \begin{bmatrix} 2 \\ 4 \\ -2 \end{bmatrix} + v \begin{bmatrix} 1 \\ -6 \\ 7 \end{bmatrix} + w \begin{bmatrix} 1 \\ 0 \\ 2 \end{bmatrix} = \begin{bmatrix} 5 \\ -2 \\ 9 \end{bmatrix} = b. $$ 


<br>

Again, the probelm is to find the combination of the column vectors on the left side that produces the vector on the right side. 
Three column vectors are represented by red, green, and blue arrows. We want to find the unknowns, $u$, $v$ and $w$. 

![intersection](/assets/images/Figure_5.png)

The solution is same as "*By rows*". The detailed methods for finding the solution will be discussed later. For now, let’s move forward! 
Our column vectors have been scaled by scalars and then addted together. We call this result **Linear Combination**. 

<br>

$$ 1 \begin{bmatrix} 2 \\ 4 \\ -2 \end{bmatrix} + 1 \begin{bmatrix} 1 \\ -6 \\ 7 \end{bmatrix} + 2 \begin{bmatrix} 1 \\ 0 \\ 2 \end{bmatrix} = \begin{bmatrix} 5 \\ -2 \\ 9 \end{bmatrix}. $$ 

<br>

---

We saw from two examples that solving by rows and by columns gives the same result. This leads to a natural question: **Will this obervation still hold when we have more than three equations and unknowns—say, $n$ of them?** 


**Yes, it is!** The row picture means finding where $n$ planes (or hyperplanes) intersect. The column picture means combining $n$ column vectors to make vector $b$. This is not just a trick of computation; it is a mathematical fact. Let’s set aside any doubt and move forward. 


Now we understand that solving a linear system is the same as finding a linear combination of column vectors. Here is one more question. **“Does such a combination actually exist? And if so, is it unique?”** — To answer this, let me introduce *the singular case*

---
**Singular cases**   
If a solution to a linear system both exists and is unique, we call the system *nonsingular*. Else, we call it a *singular system*. We now examine two representative types of singular cases.

*1. No solution*   
<br>

$$ \begin{aligned} u + v + w \quad &=\quad 2 \\ 2u \quad\quad + 3w \quad &=\quad 5 \\ 3u + v + 4w \quad &=\quad 6 \end{aligned} $$ 

<br>
The system has no solution. This occurs when the three planes($rows$) do not intersect at a single point.(We will discuss it more precisely later with *Gaussian elimination*.)   

*2. Too many solutions* 

<br>

$$ \begin{aligned} u + v + w \quad &=\quad 2 \\ 2u \quad\quad + 3w \quad &=\quad 5 \\ 3u + v + 4w \quad &=\quad 7 \end{aligned} $$ 

<br>

From the row perspective, the third equation is a linear combination of the first two equations. In this case, all points on the line of intersection between the first two planes are valid solutions. Hence, the system has infinitely many solutions. 

---

Let us now analyze these two cases from the column perspective: 

$$
u \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}
+ v \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}
+ w \begin{bmatrix} 1 \\ 3 \\ 4 \end{bmatrix}
= \mathbf{b}.
$$

*1. No solution*   
If the vector on the right side is $(2,5,6)$, it agrees with the row perspective, where the planes has no intersection point. The system has no solution. It happens when all three column vectors lie in the same plane, but $b$ does not. 

![intersection](/assets/images/Figure_6.png)

*2. Too many solutions*   
If the vector on the right side is $(2,5,7)$, it agrees with the row perspective, where the points on the intersection line are valid solutions. The system has infinitely many solutions. It happens when all three column vectors lie in the same plane, and $b$ either. 

![intersection](/assets/images/Figure_7.png) 

---

In both singular cases, a common feature emerges: *All column vectors lie within the same plane.* A simple way to detect this is to check whether there exists a nontrivial linear combination. However, as our focus here is geometric, we shall not explore this algebraic condition further. To summerize :   

<br>
**If the $n$ planes have no point in common, or infinitely many points, then the $n$ columns lie in the same plane.**   
<br>

We will focus on nonsingular cases first.We should build our familiarity with these, and later turn our attention to singular cases. However, we cannot proceed without understanding matrix notation and the method of elimination. Therefore, in the next session, we will begin exploring these essential tools.
