# Chapter 1 - Introduction

## Overview

Statistical learning refers to a vast set of tools for understanding data.
Classified as supervised or unsupervised.

<strong>Supervised</strong> - Building a statistical model for predicting, or estimating an output based on on or more input.

<strong>Unsupervised</strong> - Inputs but no supervising outputs. We can still learn relationships and structure from such data.

Provided Wage data involves predicting a continuous or quantative output. Referred to as a regression problem.

Provied Smarket data involves predicting a qualitative or categorical output. This is a classification problem.

Provided Gene Expression data involves situations where we observe input variables, with no corresponding output. This is a clustering problem.

<p>Early 19th century the method of least squares developed (Linear Regression). To predict quantitative values, linear discriminant analysis was proposed in 1936. In the 1940s, various authors put forward an alternative, logistic regression. In 1970s the term gerneralized linear model was developed to describe an entire class of statistical learning methods that include both linear and logistic regression as special cases. 1980s non linear methods were no longer computationally prohibitive, mid 1980s, classification and regression trees were developed, followed shortly by generalized additive models. Neural networks gained popularity in the 80s and support vector machines arose in the 90s. 

n - number of distinct data points, or observations in our sample.
p - number of variables available for making predictions.

$$
X = 
\begin{bmatrix}
x_{1 1} & x_{1 p} \\
x_{n 1} & x_{n p}
\end{bmatrix}
$$

$x_{ij}$ represents the value of the jth variable and for the ith observation.
We let X denote an n x p matrix whose (i, j)th elementg is $x_{ij}$.

$$
x_i = 
\begin{pmatrix}
x_i1 \\
x_i2 \\
...  \\
x_{ip}
\end{pmatrix}
$$
Vectors are by default represented as columns. Vector of lenth n is denoted in lowercase and <strong>bold.</strong> Vectors not of length n denoted in lower case normal font aswell as scalars. Matrices denoted using bold capitals.

Can only compute <strong>AB<\strong> if the number of columns opf A is the same as the number of rows of B.