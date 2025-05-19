---
layout: single
title: An Example of Gaussian Elimination
---


In this time, I will introduce the Gaussian Elimination. The discussion will proceed in the following four parts :   

1. Step - by - Step Example of Gaussian Elimination.    

2. Matrix Form of Elimination.    

3. Breakdwon of Elimination.     

4. Cost of Elimination.    

---

#### 1. Step - by - Step Example of Gaussian Elimination

The simplest way to understand the Gaussian Elimination is by example. Let's begin in three demensions: 

<br>

$$
\begin{array}{rrrrrcl}
2u &+& v  &+& w  &=& 5 \\
4u &-& 6v &+& 0w &=& -2 \\
-2u &+& 7v &+& 2w &=& 9
\end{array}
$$



<br>

We want to find the unknown values of $u$, $v$, and $w$. *It starts by subtracting muliples of the first equation from the other equations.* The goal is to eliminate $u$ from the last two equations. To do so, subtract $2$ times the first equation from the second and subtract $-1$ times the first equation from the third.

<br>

$$
\begin{array}{rrrrrcl}
\mathbf{2}u &+& v  &+& w  &=& 5 \\
      0u &-& \mathbf{8}v &-& 2w &=& -12 \\
      0u &+& 8v  &+& 3w  &=& 14
\end{array}
$$

<br>

The coefficient $2$ is the *first pivot*, and d$-8$ is the *second pivot*. We now ignore the first equation. To eliminate $v$, we add the second equation to the third.

<br>

$$
\begin{array}{rrrrrcl}
\mathbf{2}u &+& v  &+& w  &=& 5 \\
     0u &-& \mathbf{8}v &-& 2w &=& -12 \\
     0u &+& 0v &+& 1w &=& 2
\end{array}
$$

<br>

The elimination process is now complete. These whole process is called **forward elimination**. And the final form of system is *Triangular*. Now, Let's solve this system backward. The last equation gives $w =2$. Substituting into the second equation, we find $v = 1$. Then the first equation gives $u = 1$. This process is called **back-substitution**. We finally solve the system!.  

Back substitution and forward elimination together are called **Gaussian elimination**. Eliminate from forward until reach the *triangular system*, and solve it reverse order. There's one thing you need to be care. **By definition, Pivots cannot be zero. We need to divide by them.** 


---

#### 2. Matrix Form of Elimination 

One good way to write down the forward elimination steps is to include the right-hand side as an extra column. There is no need to copy $u$ and $v$ and $w$ and $=$ at every step, we left the minimum:

<br>

$$
\begin{bmatrix}
2 & 1 & 1 & 5 \\
4 & -6 & 0 & -2 \\
-2 & 7 & 2 & 9
\end{bmatrix}
\\[1.5em]
\Downarrow
\\[1.5em]
\begin{bmatrix}
2 & 1 & 1 & 5 \\
0 & -8 & -2 & -12 \\
0 & 8 & 3 & 14
\end{bmatrix}
\\[1.5em]
\Downarrow
\\[1.5em]
\begin{bmatrix}
2 & 1 & 1 & 5 \\
0 & -8 & -2 & -12 \\
0 & 0 & 1 & 2
\end{bmatrix}
$$


<br>
