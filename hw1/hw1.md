---
title: 'STA 141A Fall 2022: Homework 1'
author: 'Camden Possinger'
date: "30 September, 2022" 
output:
  html_document:
    number_sections: yes
    theme: lumen
---



The assignment has to be done in an [R Markdown](https://rmarkdown.rstudio.com) document. The assignment has to be submitted electronically on Canvas by October 3, 2022 at 11:59 PM (PT) by uploading two files:

1. an HTML or PDF file;
2. the Rmd source file.

It is possible to upload two files on Canvas. Late homework submissions will **NOT** be accepted. No submissions will be accepted by email.

Each answer has to be based on `R` code that shows how the result was obtained. `R` code has to answer the question or solve the task. For example, if you are asked to find the largest entry of a vector, `R` code has to return the largest element of the vector. If `R` code just prints all values of the vector and you determine by hand which element is the largest, this will not be accepted as an answer. No points will be given for answers that are not based on `R` code. 

There are many possible ways to write `R` code that is needed to answer the questions or do the tasks, but for some of the questions or tasks you might have to use something that has not been discussed during the lectures or the discussion sessions. You will have to come up with a solution on your own. Hints will be provided if extra packages can help, but **NO** other packages than those explicitly allowed can be used. This is a very important part of learning (if not the most important part of learning). Try to understand what you need to do to complete the task or answer the question and feel free to search the Internet for possible solutions and discuss possible solutions with other students. It is perfectly fine to ask what kind of an approach or a function other students use. However, you are not allowed to share your code or your answers with other students. Everyone has to write the code, do the tasks and answer the questions on their own. To put it simply, sharing ideas is fine, plagiarizing is not.

During discussion sessions, you may be asked to present and share your solutions with TA and other classmates.

The total number of points of this assignment is 30.

Good luck!

# Vectors and simulation
Suppose that we have:

+ four types of animals: `cat`, `dog`, `cow`, `squirrel`;
+ four possible colors: `white`, `black`, `brown`, `red`;
+ five possible attributes: `big`, `small`, `angry`, `cute`, `finicky`.

a. (1 point) Generate three random samples of size `100` from each of the three groups, so that you have a vector containing 100 animals, a vector containing 100 colors and a vactor containing 100 attributes. Call the resulting vectors of character strings as: `Animal`, `Color`, `Attribute`.



```r
set.seed(2022)
library(magrittr)

Animal <- sample(c("cat", "dog", "cow", "squirrel"), 100, TRUE)
Colors <- sample(c("white", "black", "brown", "red"), 100, TRUE)
Attribute <- sample(c("big", "small", "angry", "cute", "finicky"), 100, TRUE)
```


b. (1 point) Using the `sum()` function and a logical vector, compute the number of animals that are cats or dogs.


```r
(Animal == "dog" | Animal == "cat") %>% sum()
```

```
## [1] 42
```


c. (1 point) Compute the relative frequency of cats, dogs, cows and squirrels in the sample.


```r
Animal %>% table() / Animal %>% length()
```

```
## .
##      cat      cow      dog 
##     0.19     0.29     0.23 
## squirrel 
##     0.29
```


d. (1 point) Create a contingency table between `Animal` and `Attribute`.


```r
data.frame(
  Animal = Animal,
  Attribute = Attribute
) %>% table()
```

```
##           Attribute
## Animal     angry big cute finicky
##   cat          6   4    4       2
##   cow          7   4    4       5
##   dog          6   6    3       4
##   squirrel     7   3    3       7
##           Attribute
## Animal     small
##   cat          3
##   cow          9
##   dog          4
##   squirrel     9
```




e. (2 point) Put the three vectors together in a list of three elements called `mylist`, so that each vector is an element of the list. Use the command `length(mylist[1])` to print the length of the first vector. Is this code actually printing the length of the vector? Explain and write the correct code to print the length of the first vector of the list.


# Matrices
Consider the following system of linear equations
\begin{align*}
x_1+2x_2+3x_3+4x_4+5x_5&=7,\\
2x_1+x_2+2x_3+3x_4+4x_5&=-1,\\
3x_1+2x_2+x_3+2x_4+3x_5&=-3,\\
4x_1+3x_2+2x_3+x_4+2x_5&=5,\\
5x_1+4x_2+3x_3+2x_4+x_5&=17.
\end{align*}

a. (1 point) Create the matrix `A` and the vector `y` corresponding to the matrix equation $Ax=y$, where $A\in\mathbb R^{5\times 5}$ and $x,y\in\mathbb R^5$. 


```r
A <- matrix(c(1, 2, 3, 4, 5, 2, 1, 2, 3, 4, 3, 2, 1, 2, 3, 4, 3, 2, 1, 2, 5, 4, 3, 2, 1), nrow = 5)
y <- c(7, -1, -3, 5, 17)
```


b. (1 point) Determine if the matrix `A` is invertible using the `det()` function.

```r
A %>% det()
```

```
## [1] 48
```

A is invertible since the determinant is not 0




c. (1 point) Find the solution of the system of linear equations using the `solve()` function.


```r
solve(A, y)
```

```
## [1] -2  3  5  2 -4
```



# Data exploration and manipulation

The task is to explore the US census population estimates by county for 2015 from the package `usmap` (load the data frame from `countypop.RData`). The data frame has `3142` rows and `4` variables: `fips` is the 5-digit FIPS code corresponding to the county; `abbr` is the 2-letter state abbreviation; `county` is the full county name; `pop_2015` is the 2015 population estimate (in number of people) for the corresponding county. Each row of the data frame represents a different county or a county equivalent. For the sake of simplicity, when we say a county, that also includes a county equivalent and when we say a state, that also includes the District of Columbia. 

without creating new functions, and without using for loops, answer the following questions (using `dplyr` is allowed). 


```r
library(dplyr)
load("countypop.RData")
head(countypop)
```

```
## # A tibble: 6 × 4
##   fips  abbr  county       pop_2015
##   <chr> <chr> <chr>           <dbl>
## 1 01001 AL    Autauga Cou…    55347
## 2 01003 AL    Baldwin Cou…   203709
## 3 01005 AL    Barbour Cou…    26489
## 4 01007 AL    Bibb County     22583
## 5 01009 AL    Blount Coun…    57673
## 6 01011 AL    Bullock Cou…    10696
```


a. (1 point) Remove all the rows that contain at least one NA.


```r
countypop %<>% na.omit
```

b. (1 point) What is the total number of counties in the US?

```r
countypop$fips %>% length()
```

```
## [1] 3142
```

c. (1 point) How many unique county names are there?

```r
countypop$county %>%
  unique() %>%
  length()
```

```
## [1] 1877
```

d. (1 point) What are the top 10 most common county names?

```r
countypop %>%
  count(county, sort = TRUE) %>%
  slice(1:10)
```

```
## # A tibble: 10 × 2
##    county                n
##    <chr>             <int>
##  1 Washington County    30
##  2 Jefferson County     25
##  3 Franklin County      24
##  4 Jackson County       23
##  5 Lincoln County       23
##  6 Madison County       19
##  7 Clay County          18
##  8 Montgomery County    18
##  9 Marion County        17
## 10 Monroe County        17
```

e. (1 point) Which state has the largest number of counties? Which state has the smallest number of counties?

```r
# largest number of counties
countypop %>%
  count(abbr, sort = TRUE) %>%
  head(1)
```

```
## # A tibble: 1 × 2
##   abbr      n
##   <chr> <int>
## 1 TX      254
```

```r
# smallest number of counties
countypop %>%
  count(abbr, sort = TRUE) %>%
  tail(1)
```

```
## # A tibble: 1 × 2
##   abbr      n
##   <chr> <int>
## 1 DC        1
```

f. (1 point) What is the average population of a county in the US?

```r
countypop$pop_2015 %>%
  mean() %>%
  round()
```

```
## [1] 102298
```

g. (2 points) Which state has the largest county in terms of population? How many people live in the largest county in terms of population?

```r
countypop %>%
  arrange(desc(pop_2015)) %>%
  head(1)
```

```
## # A tibble: 1 × 4
##   fips  abbr  county       pop_2015
##   <chr> <chr> <chr>           <dbl>
## 1 06037 CA    Los Angeles… 10170292
```

h. (2 points) In order to answer the following question, combine the functions `lapply()`, `split()`, `order()`, and `tail()` (or `head()`): What is the largest county in terms of population of each of the states? 

```r
countypop %>%
  split(countypop$abbr) %>%
  lapply(function(state) {
    state[state$pop_2015 %>% order(decreasing = TRUE), c("abbr", "county", "pop_2015")] %>% head(1)
  }) %>%
  bind_rows()
```

```
## # A tibble: 51 × 3
##    abbr  county            pop_2015
##    <chr> <chr>                <dbl>
##  1 AK    Anchorage Munici…   298695
##  2 AL    Jefferson County    660367
##  3 AR    Pulaski County      392664
##  4 AZ    Maricopa County    4167947
##  5 CA    Los Angeles Coun… 10170292
##  6 CO    Denver County       682545
##  7 CT    Fairfield County    948053
##  8 DC    District of Colu…   672228
##  9 DE    New Castle County   556779
## 10 FL    Miami-Dade County  2693117
## # … with 41 more rows
```

i. (2 points) What is the average population of the 100 largest counties in the US?

```r
countypop %>%
  arrange(desc(pop_2015)) %>%
  head(100) %>%
  .$pop_2015 %>%
  mean()
```

```
## [1] 1370079
```
j. (2 points) How many people live in each of the states?

```r
countypop %>%
  group_by(abbr) %>%
  summarise("Total Population" = sum(pop_2015))
```

```
## # A tibble: 51 × 2
##    abbr  `Total Population`
##    <chr>              <dbl>
##  1 AK                738432
##  2 AL               4858979
##  3 AR               2978204
##  4 AZ               6828065
##  5 CA              39144818
##  6 CO               5456574
##  7 CT               3590886
##  8 DC                672228
##  9 DE                945934
## 10 FL              20271272
## # … with 41 more rows
```

k. (1 point) What is the average population of a county in California?


```r
countypop %>%
  filter(abbr == "CA") %>%
  .$pop_2015 %>%
  mean() %>%
  round()
```

```
## [1] 674911
```





# For loops

a. (2 points) Find the bug: The following `for` loop creates a vector that contains the sum of the first `n` numbers. In particular, if you set `n = 10`, the for loop should return a vector of size `10` containing the values 1, (1+2), (1+2+3), ...., (1+2+3+4+5+6+7+8+9+10). In words, explain why this `for` loop does not create the desired vector, and write the correct code.


```r
n <- 10
sums <- numeric(n)
for (i in 1:n) {
  sums <- sum(1:i)
  print(paste0("i: ", i))
  print(paste0("sums: ", sums))
}
sums
```

This code does not append each sum to the vector it just returns the last sum: sum(1:10)


```r
1:10 %>% sapply(function(i) {
  sum(1:i)
})
```

```
##  [1]  1  3  6 10 15 21 28 36 45 55
```


b. (2 points) In words, explain what the following code does:


```r
n <- 10
x <- 1:(2 * n)
while (x[1] < n) {
  x <- x[-1]
}
x
```

First the variable "n" is assigned the value 10 then the variable x is assigned an atomic vector containing values from 1 to 20
Then while the first value of x is less than 10 the first value of x is removed 
and the x vector is updated with its length subtracted by 1.
At the end of execution x should be the vector c(10:20)


Before running the code in R, try to read the code and understand what it does.


c. (2 points) In words, explain what the following code does:


```r
lapply(c(5, 10), rnorm, m = c(0, 10))
```

This code creates a list with length 2. 

The first element is 5 random numbers sampled from a normal distribution
with mean 0 stored in an atomic vector

The second element is 10 random numbers sampled from a normal distribution
with mean 10 stored in an atomic vector



distributun



Before running the code in `R`, try to read the code and understand what it does.



<br>
<br>
<br>
<br>
