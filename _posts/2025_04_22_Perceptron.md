---
layout : single
title : "[Implement] Perceptron to XOR"
---

In this time, we are going to implement a few simple perceptrons to the XOR gate. If you need more theoretical depth, please look at my [earlier post](https://isopink.github.io/Neural-Network/). The discussion will proceed in the following four parts: 

1. And Gate 

2. Nand Gate

3. Or Gate 

4. XOR Gate 

--- 

#### 1. And gate 

The AND gate outputs $1$ only when both input signals are $1$. The truth table is as follows:

| $x_1$ | $x_2$ | AND($x_1$, $x_2$) |
|:----:|:----:|:-------------:|
|  0 |  0 |      0      |
|  0 |  1 |      0      |
|  1 |  0 |      0      |
|  1 |  1 |      1      |

This table can be implemeted through single perceptorns with two inputs and corresponding weights and bias. I can formalize this table as below: 

<br>

$$
y = \begin{cases}
0 & \text{if } w_1 x_1 + w_2 x_2 + b \leq 0 \\
1 & \text{if } w_1 x_1 + w_2 x_2 + b > 0
\end{cases}
$$

<br>

We want to define weights and bias, $(w_1, w_2, b)$ which satisfy the AND gate. In fact, there are many combinatorial solutions, but we can define it as $(0.5, 0.5, -0.7)$. Then, we can implement it using python script as below: 

```python
import numpy as np

def AND(x1, x2):
    x = np.array([x1, x2])
    w = np.array([0.5, 0.5])
    b = -0.7
    tmp = np.sum(w*x) + b

    if tmp <= 0:
        return 0
    else:
        return 1
```

--- 

#### 2. Or gate
