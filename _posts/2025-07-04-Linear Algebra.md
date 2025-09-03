---
layout : single
title : Linear Algebra (1)
--- 

In this post, we will introduce the basics of linear lagebra. The contents are organized as follows: 

1. Systems of Linear Equations

2. Matrices

3. Solving Systems of Linear Equations 

4. Vector Spaces

---

#### 1. Systems of Linear Eqautions 

Systems of linear equations play a central part of linear algebra. Many problems can be formulated as systems of linear equations, and linear algebra gives us the tools for solving them.

## Example 1.1

A company produces products $N_1, \dots, N_n$ for which resources $R_1, \dots, R_m$ are required. To produce a unit of product $N_j$, $a_{ij}$ units of resource $R_i$ are needed, where $i = 1, \dots, m$ and $j = 1, \dots, n$. The objective is to find an optimal production plan, i.e., a plan of how many units $x_j$ of product $N_j$ should be produced if a total of $b_i$ units of resource $R_i$ are available and (ideally) no resources are left over. If we produce $x_1, \dots, x_n$ units of the corresponding products, we need a total of

<br>

$$
a_{i1}x_1 + \cdots + a_{in}x_n
\tag{2.2}
$$

<br>

many units of resource $R_i$. An optimal production plan $(x_1, \dots, x_n) \in \mathbb{R}^n$ therefore has to satisfy the following system of equations:

<br>

$$
\begin{aligned}
a_{11}x_1 + \cdots + a_{1n}x_n &= b_1 \\
&\vdots \\
a_{m1}x_1 + \cdots + a_{mn}x_n &= b_m
\end{aligned}
\tag{2.3}
$$

<br>

where $a_{ij} \in \mathbb{R}$ and $b_i \in \mathbb{R}$. 

<br>


Equation (2.3) is the general form of a *system of linear equations*, and $x_1, \dots, x_n$ are the *unknowns* of this system. Every $n$-tuple $(x_1, \dots, x_n) \in \mathbb{R}^n$ that satisfies (2.3) is a *solution* of the linear equation system.
