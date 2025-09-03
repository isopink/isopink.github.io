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

# Matrices and Their Properties

Matrices play a central role in linear algebra. They can be used to compactly represent systems of linear equations, but they also represent linear functions (linear mappings). Before we discuss these applications, let us first define what a matrix is and what operations we can perform with matrices.

---

#### 2.2 Matrices

### Definition 2.1 (Matrix)

With $m, n \in \mathbb{N}$, a real-valued $(m,n)$-matrix $A$ is an $m \times n$-tuple of elements $a_{ij}$, $i = 1, \dots, m, \; j = 1, \dots, n$, which is ordered according to a rectangular scheme consisting of $m$ rows and $n$ columns:

<br>

$$
A =
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{bmatrix}, 
\quad a_{ij} \in \mathbb{R}.
$$

<br>

By convention, $(1,n)$-matrices are called *rows* and $(m,1)$-matrices are called *columns*.  

### 2.2.1 Matrix Addition and Multiplication

The sum of two matrices $A \in \mathbb{R}^{m \times n}, \; B \in \mathbb{R}^{m \times n}$ is defined element-wise:

<br>

$$
A + B :=
\begin{bmatrix}
a_{11} + b_{11} & \cdots & a_{1n} + b_{1n} \\
\vdots & \ddots & \vdots \\
a_{m1} + b_{m1} & \cdots & a_{mn} + b_{mn}
\end{bmatrix}
\in \mathbb{R}^{m \times n}.
$$

<br>

For multiplication, the elements $c_{ij}$ of $C = AB$ are given by:

<br>

$$
c_{ij} = \sum_{l=1}^n a_{il} b_{lj}, 
\quad i = 1, \dots, m, \; j = 1, \dots, k.
$$

<br>

In compact notation:

<br>

$$
A_{m \times n} \cdot B_{n \times k} = C_{m \times k}.
$$

<br>

Matrix multiplication is **not commutative**, i.e. $AB \neq BA$ in general.

---

### Example 2.3  

For 

<br>

$$
A = \begin{bmatrix}
1 & 2 & 3 \\
2 & 3 & 1 \\
3 & 2 & 1
\end{bmatrix} \in \mathbb{R}^{3 \times 3}, 
\quad 
B = \begin{bmatrix}
0 & 2 \\
1 & 0 \\
1 & 1
\end{bmatrix} \in \mathbb{R}^{3 \times 2},
$$

<br>

we obtain

<br>

$$
AB = \begin{bmatrix}
5 & 5 \\
5 & 7 \\
3 & 7
\end{bmatrix} \in \mathbb{R}^{3 \times 2},
$$

<br>

while

<br>

$$
BA = \begin{bmatrix}
2 & 2 & 6 \\
1 & 2 & 3
\end{bmatrix} \in \mathbb{R}^{2 \times 3}.
$$

<br>

Clearly, $AB \neq BA$.

### Definition 2.2 (Identity Matrix)

The **identity matrix** $I_n \in \mathbb{R}^{n \times n}$ is defined as

<br>

$$
I_n =
\begin{bmatrix}
1 & 0 & \cdots & 0 \\
0 & 1 & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & 1
\end{bmatrix}.
$$

<br>

### Properties of Matrix Multiplication

1. **Associativity**:  
   $$
   \forall A \in \mathbb{R}^{m \times n}, B \in \mathbb{R}^{n \times p}, C \in \mathbb{R}^{p \times q}: \quad (AB)C = A(BC).
   $$

<br>

2. **Distributivity**:  
   $$
   (A + B)C = AC + BC, \quad A(B + C) = AB + AC.
   $$

<br>

3. **Identity**:  
   $$
   \forall A \in \mathbb{R}^{m \times n}: \quad I_m A = A I_n = A.
   $$

<br>

### 2.2.2 Inverse and Transpose

**Definition 2.3 (Inverse).**  
For a square matrix $A \in \mathbb{R}^{n \times n}$, if there exists a matrix $B \in \mathbb{R}^{n \times n}$ such that  

<br>

$$
AB = I_n = BA,
$$  

<br>

then $B$ is called the **inverse** of $A$ and is denoted $A^{-1}$.

Not every matrix has an inverse. If it does, it is called *regular/invertible*. Otherwise, it is *singular/non-invertible*.  

**Example 2.4 (Inverse Matrix).**  

Let  

<br>

$$
A = \begin{bmatrix}
1 & 2 & 1 \\
4 & 4 & 5 \\
6 & 7 & 7
\end{bmatrix}, 
\quad 
B = \begin{bmatrix}
-7 & -7 & 6 \\
-4 & -1 & 2 \\
5 & 2 & -4
\end{bmatrix}.
$$

<br>

Then $AB = I = BA$, i.e. $A$ and $B$ are inverses of each other.


**Definition 2.4 (Transpose).**  
For $A \in \mathbb{R}^{m \times n}$, the transpose $A^T \in \mathbb{R}^{n \times m}$ is given by $a^T_{ij} = a_{ji}$.  

Important properties:

<br>

$$
(AB)^T = B^T A^T, 
\quad (A^T)^T = A,
\quad (A^{-1})^T = (A^T)^{-1}.
$$

<br>

**Definition 2.5 (Symmetric Matrix).**  
A matrix $A \in \mathbb{R}^{n \times n}$ is symmetric if $A = A^T$.

Example of a symmetric matrix:

<br>

$$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 1 \\
0 & 1 & 0
\end{bmatrix}.
$$

<br>

### 2.2.3 Multiplication by a Scalar

For $\lambda \in \mathbb{R}$ and $C \in \mathbb{R}^{m \times n}$,  

<br>

$$
(\lambda C)_{ij} = \lambda c_{ij}.
$$

<br>

Properties:  

- $\lambda (BC) = (\lambda B) C = B(\lambda C)$  
- $(\lambda C)^T = \lambda C^T$  
- $\lambda (B + C) = \lambda B + \lambda C$  

### Example 2.5 (Distributivity)

If  

<br>

$$
C = \begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix},
$$

<br>

then  

<br>

$$
(\lambda + \psi) C =
\begin{bmatrix}
(\lambda + \psi)1 & (\lambda + \psi)2 \\
(\lambda + \psi)3 & (\lambda + \psi)4
\end{bmatrix}
=
\lambda C + \psi C.
$$

<br>

### 2.2.4 Compact Representations of Systems of Linear Equations

If we consider the system

<br>

$$
\begin{aligned}
2x_1 + 3x_2 + 5x_3 &= 1 \\
3x_1 - 2x_2 - 7x_3 &= 8 \\
9x_1 + 5x_2 - 3x_3 &= 2
\end{aligned}
$$

<br>

we can write it compactly as

<br>

$$
\begin{bmatrix}
2 & 3 & 5 \\
3 & -2 & -7 \\
9 & 5 & -3
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
x_3
\end{bmatrix}
=
\begin{bmatrix}
1 \\
8 \\
2
\end{bmatrix}.
$$

<br>

This is the matrix form $Ax = b$.

---
