---
layout : single
title : Solving Systems of Linear Equations
---

In the [earlier post](https://isopink.github.io/Linear-Algebra/), we introduced the general form of an equation system, i.e.,

$$
\begin{aligned}
a_{11}x_1 + \cdots + a_{1n}x_n &= b_1 \\
\vdots \quad & \vdots \\
a_{m1}x_1 + \cdots + a_{mn}x_n &= b_m ,
\end{aligned}
$$

where $a_{ij} \in \mathbb{R}$ and $b_i \in \mathbb{R}$ are known constants and $x_j$ are unknowns, $i=1,\dots,m$, $j=1,\dots,n$.  

Thus far, we saw that matrices can be used as a compact way of representing systems of linear equations so that we can write $Ax=b$, see this [post](https://isopink.github.io/Linear-Algebra(2)/). Moreover, we defined basic matrix operations, such as addition and multiplication of matrices. 

In the following, we will focus on solving systems of linear equations and provide an algorithm for finding the inverse of a matrix. The table of contents are organized as follows: 

1. Particular and General Solution
2. Elementary Transformations
3. The Minus-1 Trick
4. Calculating the Inverse
5. Algorithms for Solving Linear System

---

### 1. Particular and General Solution

Before discussing how to generally solve systems of linear equations, let us have a look at an example. Consider the system of equations

$$
\begin{bmatrix}
1 & 0 & 8 & -4 \\
0 & 1 & 2 & 12
\end{bmatrix}
\begin{bmatrix}
x_1 \\ x_2 \\ x_3 \\ x_4
\end{bmatrix}
=
\begin{bmatrix}
42 \\ 8
\end{bmatrix}
$$

The system has two equations and four unknowns. Therefore, in general we would expect infinitely many solutions. This system of equations is in a particularly easy form, where the first two columns consist of a $1$ and a $0$.  

We want to find scalars $x_1, \dots, x_4$ such that $\sum_{i=1}^4 c_i x_i = b$, where $c_i$ is the $i$-th column of the matrix and $b$ the right-hand side of (2.38). A solution to the problem can be found immediately by taking $42$ times the first column and $8$ times the second column so that

$$
b = 
\begin{bmatrix} 42 \\ 8 \end{bmatrix}
= 42 \begin{bmatrix} 1 \\ 0 \end{bmatrix}
+ 8 \begin{bmatrix} 0 \\ 1 \end{bmatrix}
$$

Therefore, a solution is $[42, 8, 0, 0]^T$. This solution is called a **particular solution** or **special solution**.  

However, this is not the only solution. To capture all the other solutions, we need to be creative in generating $0$ in a non-trivial way using the columns of the matrix. Adding $0$ to our special solution does not change the special solution.  

For instance, by using the third column we can express:

$$
\begin{bmatrix} 8 \\ 2 \end{bmatrix}
= 8 \begin{bmatrix} 1 \\ 0 \end{bmatrix}
+ 2 \begin{bmatrix} 0 \\ 1 \end{bmatrix}
$$

Thus,

$$
\begin{bmatrix}
1 & 0 & 8 & -4 \\
0 & 1 & 2 & 12
\end{bmatrix}
\begin{bmatrix}
8 \\ 2 \\ -1 \\ 0
\end{bmatrix}
= 0
$$

Similarly, with the fourth column:

$$
\begin{bmatrix}
1 & 0 & 8 & -4 \\
0 & 1 & 2 & 12
\end{bmatrix}
\begin{bmatrix}
-4 \\ 12 \\ 0 \\ 1
\end{bmatrix}
= 0
$$

Thus the general solution is

$$
x \in \mathbb{R}^4 : x = 
\begin{bmatrix} 42 \\ 8 \\ 0 \\ 0 \end{bmatrix}
+ \lambda_1 \begin{bmatrix} 8 \\ 2 \\ -1 \\ 0 \end{bmatrix}
+ \lambda_2 \begin{bmatrix} -4 \\ 12 \\ 0 \\ 1 \end{bmatrix},
\quad \lambda_1, \lambda_2 \in \mathbb{R}
$$

The general approach we followed consisted of three steps: 

1. Find a particular solution to $Ax=b$.
2. Find all solutions to $Ax=0$.
3. Combine the solutions from steps 1 and 2 to get the general solution.  

Neither the general nor the particular solution is unique.  

---

### 2. Elementary Transformations

Key to solving a system of linear equations are **elementary transformations** that keep the solution set the same but transform the system into a simpler form:

- Exchange of two equations (rows in the matrix).  
- Multiplication of an equation (row) with a constant $\lambda \in \mathbb{R} \setminus \{0\}$.  
- Addition of two equations (rows).

<br>

<div style="border: 2px solid #ddd; padding: 15px; border-radius: 6px; background: #fafafa;"> 

For $a \in \mathbb{R}$, consider

$$
\begin{aligned}
-2x_1 + 4x_2 - 2x_3 - x_4 + x_5 &= -3 \\
4x_1 + 8x_2 + 3x_3 - 3x_4 + 2x_5 &= 0 \\
x_1 - 2x_2 + x_3 - 3x_4 + 4x_5 &= 1 \\
x_1 - 2x_2 - 3x_4 + 4x_5 &= a 
\end{aligned}
$$

We build the augmented matrix $[A|b]$:

$$
\begin{bmatrix}
-2 & 4 & -2 & -1 & 1 & -3 \\
4 & 8 & 3 & -3 & 2 & 0 \\
1 & -2 & 1 & -3 & 4 & 1 \\
1 & -2 & 0 & -3 & 4 & a
\end{bmatrix}
$$

Applying row swaps and transformations, we eventually obtain the row-echelon form (REF):

$$
\begin{bmatrix}
1 & -2 & -1 & -1 & 1 & 0 \\
0 & 0 & 1 & -3 & 2 & 1 \\
0 & 0 & 0 & 0 & 1 & -a \\
0 & 0 & 0 & 0 & 0 & a+1
\end{bmatrix}
$$

Only for $a=-1$ the system is solvable. A particular solution is

$$
x = \begin{bmatrix} 2 \\ 0 \\ -1 \\ 0 \\ 1 \end{bmatrix}
$$

The general solution is

$$
x \in \mathbb{R}^5 : 
x = \begin{bmatrix} 2 \\ 0 \\ -1 \\ 0 \\ 1 \end{bmatrix}
+ \lambda_1 \begin{bmatrix} 1 \\ 0 \\ 0 \\ 1 \\ 0 \end{bmatrix}
+ \lambda_2 \begin{bmatrix} 0 \\ 1 \\ 0 \\ 2 \\ 1 \end{bmatrix},
\quad \lambda_1, \lambda_2 \in \mathbb{R}
$$

</div>

<br>

◦ **Definition (Row-Echelon Form)**  

A matrix is in row-echelon form if:

- All rows that contain only zeros are at the bottom.  
- In each non-zero row, the first non-zero entry (pivot) lies to the right of the pivot in the row above.  
- The pivot is the only nonzero entry in its column.  

---

**Remark (Basic and Free Variables).**  
Variables corresponding to pivots are **basic variables**. Others are **free variables**.  

**Remark (Gaussian Elimination).**  
Gaussian elimination is an algorithm that performs elementary transformations to bring a system into reduced row-echelon form.

---

<div style="border: 2px solid #ddd; padding: 15px; border-radius: 6px; background: #fafafa;">

**Example 2.7 (Reduced Row Echelon Form).**  

Verify whether  

$$
A = \begin{bmatrix}
1 & 3 & 0 & 0 & 9 \\
0 & 0 & 1 & 0 & -4 \\
0 & 0 & 0 & 1 & -4
\end{bmatrix}
\tag{2.49}
$$

is in reduced row echelon form.

</div>

---

## 2.3.3 The Minus-1 Trick

We introduce a practical trick for reading out solutions $x$ of a homogeneous system $Ax=0$ where $A \in \mathbb{R}^{m \times n}$.  

We assume $A$ is in reduced row-echelon form without all-zero rows. Extend $A$ to an $n \times n$ matrix by adding rows with $-1$ in the pivot column:

$$
\begin{bmatrix}
0 & 0 & 1 & * & \cdots \\
0 & 0 & 0 & 1 & * \\
\vdots & \vdots & \vdots & \vdots & \vdots \\
0 & 0 & 0 & 0 & 1
\end{bmatrix}
\tag{2.51}
$$

The columns with $-1$ give the solution vectors.

<div style="border: 2px solid #ddd; padding: 15px; border-radius: 6px; background: #fafafa;">

**Example 2.8 (Minus-1 Trick).**  

For  

$$
A = \begin{bmatrix}
1 & 3 & 0 & 0 & 9 \\
0 & 0 & 1 & 0 & -4 \\
0 & 0 & 0 & 1 & -4
\end{bmatrix},
\tag{2.53}
$$

the augmented $\tilde{A}$ is

$$
\tilde{A} = \begin{bmatrix}
1 & 3 & 0 & 0 & 9 \\
0 & 0 & 1 & 0 & -4 \\
0 & 0 & 0 & 1 & -4 \\
0 & 0 & 0 & 0 & -1 \\
0 & 0 & 0 & 0 & -1
\end{bmatrix}.
\tag{2.54}
$$

Thus the general solution is

$$
x \in \mathbb{R}^5 : 
x = \lambda_1 \begin{bmatrix} 3 \\ -1 \\ 0 \\ 0 \\ 0 \end{bmatrix}
+ \lambda_2 \begin{bmatrix} 9 \\ 0 \\ -4 \\ -4 \\ 1 \end{bmatrix}.
\tag{2.55}
$$

</div>

---

## 2.3.4 Algorithms for Solving Systems

To compute the inverse $A^{-1}$ of $A \in \mathbb{R}^{n \times n}$, we solve $AX=I_n$. This can be done by augmenting $A$ with $I_n$ and applying Gaussian elimination.

<div style="border: 2px solid #ddd; padding: 15px; border-radius: 6px; background: #fafafa;">

**Example 2.9 (Calculating an Inverse Matrix by Gaussian Elimination).**  

$$
A = \begin{bmatrix}
1 & 0 & 2 \\
1 & 1 & 0 \\
0 & 2 & 0
\end{bmatrix}.
\tag{2.57}
$$

Applying Gaussian elimination to $[A|I]$, we obtain

$$
A^{-1} = \begin{bmatrix}
-1 & 2 & -2 \\
2 & -1 & 2 \\
1 & -1 & 1
\end{bmatrix}.
\tag{2.58}
$$

</div>

---

**Further Algorithms.**  
- **Gaussian elimination** is efficient but scales poorly with large systems.  
- **Iterative methods** (Richardson, Jacobi, Gauss–Seidel, Krylov methods) are better suited for very large systems.  
- **Least squares solutions** can be found with the Moore–Penrose pseudoinverse $A^+ = (A^T A)^{-1} A^T$.  

---

