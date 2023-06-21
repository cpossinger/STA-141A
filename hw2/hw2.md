---
title: 'STA 141A Fall 2022: Homework 2'
author: ''
date: ""
output:
  html_document:
    number_sections: no
  pdf_document: default
editor_options: 
  markdown: 
    wrap: 72
---

The assignment has to be done in an [R
Markdown](https://rmarkdown.rstudio.com) document. The assignment has to
be submitted electronically on Canvas until the deadline of October 21,
2022 at 11:59 PM by uploading two files:

1.  an HTML or PDF file;
2.  the Rmd source file.

It is possible to upload two files on Canvas. Late homework submissions will **NOT** be accepted. No submissions will be accepted by email.

Each answer has to be based on `R` code that shows how the result was
obtained. `R` code has to answer the question or solve the task. For
example, if you are asked to find the largest entry of a vector, `R`
code has to return the largest element of the vector. If `R` code just
prints all values of the vector and you determine by hand which element
is the largest, this will not be accepted as an answer. No points will
be given for answers that are not based on `R` code.

There are many possible ways to write `R` code that is needed to answer
the questions or do the tasks, but for some of the questions or tasks
you might have to use something that has not been discussed during the
lectures or the discussion sessions. You will have to come up with a
solution on your own. Hints will be provided if extra packages can help,
but **NO** other packages than those explicitly allowed can be used.
This is a very important part of learning (if not the most important
part of learning). Try to understand what you need to do to complete the
task or answer the question and feel free to search the Internet for
possible solutions and discuss possible solutions with other students.
It is perfectly fine to ask what kind of an approach or a function other
students use. However, you are not allowed to share your code or your
answers with other students. Everyone has to write the code, do the
tasks and answer the questions on their own. To put it simply, sharing
ideas is fine, plagiarizing is not.

The total number of points of this assignment is 30.

Good luck!

# 1. Examining the distribution of the data

Go to [UCI Machine learning
repository](https://archive.ics.uci.edu/ml/datasets/Wine+Quality) and
download the data on the white wine quality. This page contains also the
background information on the data. In our analysis we will only
consider the following variables:\
`pH`: pH level\
`quality`: Wine quality in a score between 0 and 10\

1.  Read the data into R. Add to the data frame a new binary variable
    good which is 1 if quality \> 5 and 0 otherwise (1 point).

Below, consider the `pH` value for good, bad and all wines separately
and put all three graphics in each exercise in one plot.

2.  Calculate the summary statistics for `pH` for good, bad and all
    wines separately, that is: mean, median, standard deviation,
    interquartile range, minimum and maximum of both samples. Display
    the results in a table and comment on the differences between both
    groups, if any (1 point).

3.  Plot a histogram of `pH` for good, bad and all wines and add to the
    plots a normal density, estimating the parameters from the data.
    Produce same histograms with corresponding normal densities for good
    and bad wines separately. Do you observe any differences in the
    distributions? (2 point).

4.  Generate QQ-plots with `ggplot` of `pH` for good, bad and all wines
    to compare empirical quantiles of the samples to the theoretical
    quantiles of a normal distribution. Add a angle bisector line to the
    plot. Do you think all samples follow a normal distribution? (1
    points).

# 2. Simulation study

Suppose that $X_1,\ldots,X_n$ are independent and identically
distributed (iid) binomial random variables such that $$
  P(X_i=x\mid k,p)
  ={k\choose x}p^x(1-p)^{k-x},\quad x=0,1,\ldots,k
$$ for all $i=1,\ldots,n$. Assume that both $k$ and $p$ are unknown and
use the method of moments to obtain point estimators of both parameters.
This somewhat unusual application of the binomial model has been used to
estimate crime rates for crimes that are known to have many unreported
occurrences. For such a crime, both the true reporting rate, $p$, and
the total number of occurrences, $k$, are unknown. Equating the first
two sample moments to those of the population yields the system of
equations $$
  \bar X=kp
  \quad\text{and}\quad
  \frac1n\sum_{i=1}^nX_i^2=kp(1-p)+k^2p^2,
$$ where $\bar X$ is the sample mean. Solving for $k$ and $p$ leads to
$$
  \hat k=\frac{\bar X^2}{\bar X-(1/n)\sum_{i=1}^n(X_i-\bar X)^2}
  \quad\text{and}\quad
  \hat p=\frac{\bar X}{\hat k}.
$$ It is difficult to analyze the performance of $\hat k$ and $\hat p$
analytically so you are asked to perform a simulation study using `R`.
The idea is to generate random samples and investigate the performance
of $\hat k$ and $\hat p$ using random samples.

1.  Generate a single simple random sample of length `n <- 50` from the
    binomial distribution with the parameters `k <- 10`, `p <- 0.4` (1
    point).

2.  Write a function that takes a sample as its input and returns a
    vector containing the estimates of `k` and `p` given above (3
    points).

3.  Generate `N <- 1000` samples of size `n <- 50` (as in the first
    question) and calculate `N <- 1000` estimates of $k$ and `N <- 1000`
    estimates of $p$ (4 points if no loops are used in the code, 2
    points if any loop (`for`, `while`, `repeat`, etc.) is used in the
    code ).

4.  Repeat Question 3 when `n <- 100` and when `n <- 250` (2 points).

5.  Estimate the bias and the mean squared error (MSE), 
$$MSE(k,\hat k) = \sum_{i=1}^n(k - \hat k)^2,$$ 
of $\hat k$ and
    the bias and the MSE of $\hat p$ for each sample size (`n <- 50`,
    `n <- 100` and `n <- 250`). Do the estimators seem to overestimate
    or underestimate the parameters? How do the bias and the MSE change
    when the sample size increases? (3 points).

6.  

    a.  Make a single plot using `ggplot2` that contains three box plots
        of the estimates of the parameter `k` when `n <- 50`,
        `n <- 100`, `n <- 250` (the first from the left box plot has to
        describe the estimates when `n <- 50`, the second from the left
        box plot has to describe the estimates when `n <- 100` and the
        third from the left box plot has to describe the estimates
        `n <- 250`). Include the true value of the parameter as a
        horizontal line (`geom_hline()` and use the argument `color`)
        and label the plot appropriately (4 points).

    b.  $\hat k$ can obtain values that are far away from the true value
        of the parameter when the sample size is small and the box plots
        might not be particularly informative in such a situation.
        Remove the estimates from the plot that are outside of the
        interval $[0,50]$ so that the box plots are more informative (4
        points).

    c.  Make the same plot with three box plots for the estimates of the
        parameter `p` (b part does not apply here) (2 points).

    d.  Describe how both of these plots change when the sample size
        increases (2 points).
