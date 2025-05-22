---
layout: single
title: "Lecture 3 : The Linear Model I"
---

In this time, I am going to introduce some Linear Model. This part is not directly related to the previous or next chapters.
Nevertheless, it will be used for deeper concepts later. The discussion will proceed in the following four parts :   

1. Input representation

2. Linear Classification    

3. Linear Regression     

4. Nonlinear Transformation    

---

#### 1. Input representation 

Let’s begin with an example of classifying handwritten digits. Each image is made up of 16 by 16 pixels. First, we need to convert the image into numerical data. If we treat this as $256 + 1$ inputs and a corresponding weight vector, the input and weight vector would look like this: 

<br>

$$
\mathbf{X} = (x_0, x_1, x_2, \cdots, x_{256})
$$

<br>

<br>

$$
\mathbf{W} = (w_0, w_1, w_2, \cdots, w_{256})
$$

<br>

Intuitively, you can tell that this will involve a lot of computation. We should extract useful information, such as intensity and symmetry. Simply put, intensity is the number of black pixels, and symmetry is whether the input data is symmetric. Then, the input and weight model can be simplified as follows:

<br>

$$
\mathbf{X} = (x_0, x_1, x_2) \quad \mathbf{W} = (w_0, w_1, w_2) 
$$

<br>

*Optional*: We define asymmetry as the average absolute difference between an image and its flipped versions, and symmetry as the negation of asymmetry. Digit 1 would result in a higher symmetry value. 

---

#### 2. Linear Classification

