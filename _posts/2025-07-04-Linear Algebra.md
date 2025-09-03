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

<br>

##### 1.1 General Example

<br>

A company produces products $N_1, \dots, N_n$ for which resources $R_1, \dots, R_m$ are required.  
To produce a unit of product $N_j$, $a_{ij}$ units of resource $R_i$ are needed, where $i = 1, \dots, m$ and $j = 1, \dots, n$.

The objective is to find an optimal production plan, i.e., a plan of how many units $x_j$ of product $N_j$ should be produced if a total of $b_i$ units of resource $R_i$ are available and (ideally) no resources are left over. If we produce $x_1, \dots, x_n$ units of the corresponding products, we need a total of

<br>

$$
a_{i1}x_1 + \cdots + a_{in}x_n
\tag{1.2}
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
\tag{1.3}
$$

<br>

where $a_{ij} \in \mathbb{R}$ and $b_i \in \mathbb{R}$. Equation (1.3) is the general form of a *system of linear equations*, and $x_1, \dots, x_n$ are the *unknowns* of this system. Every $n$-tuple $(x_1, \dots, x_n) \in \mathbb{R}^n$ that satisfies (1.3) is a *solution* of the linear equation system.

<br>

##### 1.2 Singular Example

<br>

The system of linear equations  

<br>

$$
\begin{aligned}
x_1 + x_2 + x_3 &= 3 \quad (1) \\
x_1 - x_2 + 2x_3 &= 2 \quad (2) \\
2x_1 \;\;\;\;\;\;\; + 3x_3 &= 1 \quad (3)
\end{aligned}
\tag{1.4}
$$

<br>

has *no solution*: Adding the first two equations yields $2x_1 + 3x_3 = 5$, which contradicts the third equation (3). Let us have a look at the system of linear equations 

<br>

$$
\begin{aligned}
x_1 + x_2 + x_3 &= 3 \quad (1) \\
x_1 - x_2 + 2x_3 &= 2 \quad (2) \\
\;\;\;\;\;\; 2x_1 + 3x_3 &= 2 \quad (3)
\end{aligned}
\tag{1.5}
$$

<br>

From the first and third equation, it follows that $x_1 = 1$.  
From (1)+(2), we get $2x_1 + 3x_3 = 5$, i.e., $x_3 = 1$.  
From (3), we then get that $x_2 = 1$.  

Therefore, $(1,1,1)$ is the only possible and *unique solution*  
(verify that $(1,1,1)$ is a solution by plugging in).  

As a third example, we consider  

<br>

$$
\begin{aligned}
x_1 + x_2 + x_3 &= 3 \quad (1) \\
x_1 - x_2 + 2x_3 &= 2 \quad (2) \\
2x_1 \;\;\;\;\;\;\; + 3x_3 &= 5 \quad (3)
\end{aligned}
\tag{1.6}
$$

<br>

Since (1)+(2)=(3), we can omit the third equation (*redundancy*).  
From (1) and (2), we get $2x_1 = 5 - 3x_3$ and $2x_2 = 1 + x_3$.  

We define $x_3 = a \in \mathbb{R}$ as a free variable,  
such that any triplet  

<br>

$$
\left( \tfrac{5}{2} - \tfrac{3}{2}a, \; \tfrac{1}{2} + \tfrac{1}{2}a, \; a \right), 
\quad a \in \mathbb{R}
\tag{1.7}
$$

<br>

is a solution of the system of linear equations, i.e., we obtain a solution set that contains *infinitely many* solutions.  

<br>

##### 1.3. Compact Notation 

<br>

For a systematic approach to solving systems of linear equations, we will introduce a useful compact notation.  
We collect the coefficients $a_{ij}$ into vectors and collect the vectors into matrices.  
In other words, we write the system from (2.3) in the following form:

$$
x_1 
\begin{bmatrix}
a_{11} \\
\vdots \\
a_{m1}
\end{bmatrix}
+ x_2
\begin{bmatrix}
a_{12} \\
\vdots \\
a_{m2}
\end{bmatrix}
+ \cdots + x_n
\begin{bmatrix}
a_{1n} \\
\vdots \\
a_{mn}
\end{bmatrix}
=
\begin{bmatrix}
b_1 \\
\vdots \\
b_m
\end{bmatrix}
\tag{2.9}
$$

---

$$
\Longleftrightarrow
\begin{bmatrix}
a_{11} & \cdots & a_{1n} \\
\vdots & \ddots & \vdots \\
a_{m1} & \cdots & a_{mn}
\end{bmatrix}
\begin{bmatrix}
x_1 \\
\vdots \\
x_n
\end{bmatrix}
=
\begin{bmatrix}
b_1 \\
\vdots \\
b_m
\end{bmatrix}
\tag{2.10}
$$

In the following, we will have a close look at these *matrices* and define computation rules.  
We will return to solving linear equations in Section 2.3.

