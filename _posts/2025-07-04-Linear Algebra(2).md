---
layout: single
title: Matrices and Their Properties
---

Matrices play a central role in linear algebra. They can be used to represent systems of linear equations in a compact form, and they also represent linear functions (linear mappings). Before discussing these applications, let us first define what a matrix is and what operations can be performed with matrices. The contents of this post are organized as follows: 

1. Matrix  
2. Matrix Addition and Multiplication
3. Identity Matrix
4. Properties of Matrix Multiplication
5. Inverese and Transpose
6. Symmetric Matrix
7. Multiplication by a Scalar
8. Linear Systems as Matrices

---
### 1. Definition of a Matrix 

<br>

**Definition (Matrix)**

With $m, n \in \mathbb{N}$, a real-valued $(m,n)$-matrix $A$ is an $m \times n$-tuple of elements $a_{ij}$, $i = 1, \dots, m, \; j = 1, \dots, n$, which is ordered according to a rectangular scheme consisting of $m$ rows and $n$ columns:

$$
A =
\begin{bmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{bmatrix}, 
\quad a_{ij} \in \mathbb{R}
$$

By convention, $(1,n)$-matrices are called *rows* and $(m,1)$-matrices are called *columns*.  

---

### 2. Matrix Addition and Multiplication

<br>

The sum of two matrices $A \in \mathbb{R}^{m \times n}, \; B \in \mathbb{R}^{m \times n}$ is defined element-wise:

$$
A + B :=
\begin{bmatrix}
a_{11} + b_{11} & \cdots & a_{1n} + b_{1n} \\
\vdots & \ddots & \vdots \\
a_{m1} + b_{m1} & \cdots & a_{mn} + b_{mn}
\end{bmatrix}
\in \mathbb{R}^{m \times n}
$$

For multiplication, the elements $c_{ij}$ of $C = AB$ are given by:

$$
c_{ij} = \sum_{l=1}^n a_{il} b_{lj}, 
\quad i = 1, \dots, m, \; j = 1, \dots, k
$$

In compact notation:

$$
A_{m \times n} \cdot B_{n \times k} = C_{m \times k}
$$

Matrix multiplication is **not commutative**, i.e., in general $AB \neq BA$.

<div style="border: 2px solid #ddd; padding: 15px; border-radius: 6px; background: #fafafa;">

For  

$$
A = \begin{bmatrix}
1 & 2 & 3 \\
2 & 3 & 1 \\
3 & 2 & 1
\end{bmatrix}, 
\quad 
B = \begin{bmatrix}
0 & 2 \\
1 & 0 \\
1 & 1
\end{bmatrix},
$$

we obtain  

$$
AB = \begin{bmatrix}
5 & 5 \\
5 & 7 \\
3 & 7
\end{bmatrix}, 
\quad
BA = \begin{bmatrix}
2 & 2 & 6 \\
1 & 2 & 3
\end{bmatrix}
$$  

Clearly, $AB \neq BA$.

</div>

---
### 3. Identity Matrix

<br>

**Definition (Identity Matrix)**

The identity matrix $I_n \in \mathbb{R}^{n \times n}$ is defined as

$$
I_n =
\begin{bmatrix}
1 & 0 & \cdots & 0 \\
0 & 1 & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \cdots & 1
\end{bmatrix}
$$

---
### 4. Properties of Matrix Multiplication

<br>

1. **Associativity**:  
   $$
   \forall A \in \mathbb{R}^{m \times n}, B \in \mathbb{R}^{n \times p}, C \in \mathbb{R}^{p \times q}: \quad (AB)C = A(BC)
   $$

2. **Distributivity**:  
   $$
   (A + B)C = AC + BC, \quad A(B + C) = AB + AC
   $$

3. **Identity**:  
   $$
   \forall A \in \mathbb{R}^{m \times n}: \quad I_m A = A I_n = A
   $$

---
### 5. Inverse and Transpose

<br>

**Definition (Inverse)**

For a square matrix $A \in \mathbb{R}^{n \times n}$, if there exists a matrix $B \in \mathbb{R}^{n \times n}$ such that  

$$
AB = I_n = BA,
$$  

then $B$ is called the **inverse** of $A$ and is denoted $A^{-1}$.

Not every matrix has an inverse. If it does, it is called *regular/invertible*. Otherwise, it is *singular/non-invertible*.  

<div style="border: 2px solid #ddd; padding: 15px; border-radius: 6px; background: #fafafa;">

Let  

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

Then $AB = I = BA$, i.e., $A$ and $B$ are inverses of each other.

</div>

**Definition (Transpose)**

For $A \in \mathbb{R}^{m \times n}$, the transpose $A^T \in \mathbb{R}^{n \times m}$ is given by $a^T_{ij} = a_{ji}$.  

Some important properties are:

$$
(AB)^T = B^T A^T, 
\quad (A^T)^T = A,
\quad (A^{-1})^T = (A^T)^{-1}
$$

---

### 6. Symmetric Matrix

<br>

**Definition (Symmetric Matrix)**

A matrix $A \in \mathbb{R}^{n \times n}$ is symmetric if $A = A^T$.

Example of a symmetric matrix:

$$
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 1 \\
0 & 1 & 0
\end{bmatrix}
$$

---
### 7. Multiplication by a Scalar

<br>

For $\lambda \in \mathbb{R}$ and $C \in \mathbb{R}^{m \times n}$,  

$$
(\lambda C)_{ij} = \lambda c_{ij}
$$

Properties:  

- $\lambda (BC) = (\lambda B) C = B(\lambda C)$  
- $(\lambda C)^T = \lambda C^T$  
- $\lambda (B + C) = \lambda B + \lambda C$  

<div style="border: 2px solid #ddd; padding: 15px; border-radius: 6px; background: #fafafa;">

If  

$$
C = \begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix},
$$

then  

$$
(\lambda + \psi) C =
\begin{bmatrix}
(\lambda + \psi)1 & (\lambda + \psi)2 \\
(\lambda + \psi)3 & (\lambda + \psi)4
\end{bmatrix}
=
\lambda C + \psi C
$$

</div>

---
### 8. Linear Systems as Matrices

<br>

If we consider the system

$$
\begin{aligned}
2x_1 + 3x_2 + 5x_3 &= 1 \\
3x_1 - 2x_2 - 7x_3 &= 8 \\
9x_1 + 5x_2 - 3x_3 &= 2
\end{aligned}
$$

we can write it compactly as

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

This is the matrix form $Ax = b$. 
