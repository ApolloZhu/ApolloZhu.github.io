---
title: Vector & Matrix Basics
date: 2017-06-16 11:58:00
updated: 2018-01-29 23:18:14
keywords:
tags:
- English
- AI/ML
categories:
- 数学
---

$$(x,y)=x\times\hat{i}+y\times\hat{j}=\begin{bmatrix}x\\y\end{bmatrix}$$
Addition: adding each of the components separately.
Scalar multiplication: multiplying each of the components with the scalar.
Magnitude/Length of $\vec{v}$: $\begin{Vmatrix}\vec{v}\end{Vmatrix}=\sqrt{comp_0^2+\ldots}$
Unit vector of $\vec{v}$: $\vec{u}=\frac{\vec{v}}{\begin{Vmatrix}\vec{v}\end{Vmatrix}}$, of length 1
Matrix multiplication: $m_1\times m_2$ is undefined unless $m_1$.row = $m_2$.column and $m_1$.column = $m_2$.row, resulting in a matrix $m_3$ of size $m_1$.row $\times$ $m_2$.column.

```swift
var m3 = [[Double]](
    repeating: [Double](repeating: 0, count: m2.column),
    count: m1.row
)
for i in m1.row {
    for j in m2.column {
        for m in m1.column {
            m3[i][j] += m1[i][m] * m2[m][j]
        }
    }
}
```
