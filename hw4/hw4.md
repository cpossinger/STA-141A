---
title: 'STA 141A Fall 2022: Homework 4'
output: html_document
date: ""
---

The assignment has to be done in an [R Markdown](https://rmarkdown.rstudio.com) document. The assignment has to be submitted electronically on Canvas by November 18, 2022 at 11:59 PM (PT) by uploading two files:

1. an HTML or PDF file;
2. the Rmd source file.

It is possible to upload two files on Canvas. Late homework submissions will **NOT** be accepted. No submissions will be accepted by email.

Each answer has to be based on `R` code that shows how the result was obtained. `R` code has to answer the question or solve the task. For example, if you are asked to find the largest entry of a vector, `R` code has to return the largest element of the vector. If `R` code just prints all values of the vector and you determine by hand which element is the largest, this will not be accepted as an answer. No points will be given for answers that are not based on `R` code. 

There are many possible ways to write `R` code that is needed to answer the questions or do the tasks, but for some of the questions or tasks you might have to use something that has not been discussed during the lectures or the discussion sessions. You will have to come up with a solution on your own. Hints will be provided if extra packages can help, but **NO** other packages than those explicitly allowed can be used. This is a very important part of learning (if not the most important part of learning). Try to understand what you need to do to complete the task or answer the question and feel free to search the Internet for possible solutions and discuss possible solutions with other students. It is perfectly fine to ask what kind of an approach or a function other students use. However, you are not allowed to share your code or your answers with other students. Everyone has to write the code, do the tasks and answer the questions on their own. To put it simply, sharing ideas is fine, plagiarizing is not.

During discussion sessions, you may be asked to present and share your solutions with TA and other classmates.

The total number of points of this assignment is 30.

Good luck!


# Cross-validation

We will perform cross-validation on a simulated data set.


```r
x <- runif(100)
y <- 1 + x - x^2 + rnorm(100, 0, 0.1)
```

a. (1.5 points) Describe the model used to generate the data in equation form. What is the sample size $n$? 
The model in equation form is: 

\[y ~ 1 + x - x^2 + \epsilon \]
\[n = 100\]

where epsilon is normally distributed with mean 0 and standard deviation 0.1 

b. (1.5 points) Create a scatterplot of X against Y . Comment on what you find. 


c. (2 points) Use `lm()` to fit 3 models below. Print the summary tables for 3 fitted models and comment on what you find.

- Model I: $Y = \beta_0 + \beta_1 X + \epsilon$
- Model II: $Y = \beta_0 + \beta_1 X + \beta_2 X^2 + \epsilon$
- Model III: $Y = \beta_0 + \beta_1 X + \beta_2 X^2 + \beta_3 X^3 + \epsilon$


d. (2 points) Calculate the leave-one-out-cross-validation mean squared error for each model.


e. (2 points) Calculate the k-fold-cross-validation ($k=10$) mean squared error for each model.


f. (1 point) Based on your results in (d) and (e), which model has the least cross-validation error? Briefly explain why.



# Random Number Generation

a. Simulate `N = 1000` binomial random variables $B(n = 10; p = 0.4)$ using three approaches:  inversion
method, by simulating corresponding Bernoulli random variables by inversion method
and using R function `rbinom`. Plot the empirical probability density functions of all
three samples on one panel. Comment on the results.
b. The aim is to simulate `N = 10 000` standard normal distributed random variables
with density $f(x) = (2\pi)^{-0.5} exp(x^2/2)$ using accept-reject method and a generator
for uniform random variables only. As a candidate density g use the density of the
standard Cauchy distribution $g(x) = \{\pi(1 + x^2)\}^{-1}$.
- Choose a value of the constant $c$, such that $f(x) \leq cg(x)$. 
- Obtain `N` standard normal random variables using the accept-reject method, generating Cauchy distributed random variables using inversion method. Compare
estimated and theoretical acceptance probabilities. Plot a histogram of the obtained sample and add the standard normal density to the plot. Make a QQ-plot.
Comment on the results.
- Is it possible to simulate from the standard Cauchy density using
the accept-reject method with a standard normal candidate density? 























