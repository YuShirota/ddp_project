---
title       : Devoleping Data Products, Course Project
subtitle    : calculation of positive/negative predictive values
author      : YS
job         : student
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 

## How correct is my test result??

Clinical test is used to determine if a person has a certain disease or not.
Usually property of a test is described using sensitivity and specificity.

1. Sensitivity is the probability where a person gets the positive test results if the person actually has the disease.
2. Specificity indicates the probability where a person gets the negative test results if the person does not have the disease.

The problem here is, high sensitivity does not necessarily mean that positive test
results in higher probability of having the disease.

--- &twocol

## Illustration of the problem.
These two tables show positive and negative predictive values 
(PPV and NPV respectively) from different
populations with different prevalence (also known as pre-test probability). Note
that sensitivity and specificity are 0.9 in both cases.

You can see how PPV and NPV differs with different prevalences.

*** =left
Low prevalence( 0.001)

```
##        Disease + Disease -
## Test +       0.9       0.1
## Test -      99.9     899.1
```

```
##         PPV         NPV 
## 0.008928571 0.000111210
```

*** =right
High prevalence (0.1)

```
##        Disease + Disease -
## Test +        90        10
## Test -        90       810
```

```
##        PPV        NPV 
## 0.50000000 0.01219512
```

---

## Functions in my shiny app
This shiny app calculates PPV and NPV based on
three parameters: sensisivity, specificity and prevalence.

It's done using the following functions

```r
positivePV <- function(sens, spec, prev){
    sens * prev / (sens * prev + (1 - spec) * (1 - prev))
}

negativePV <- function(sens, spec, prev) {
    spec * (1- prev) / ((1 - sens) * prev + spec * (1 - prev)) 
}
```

---

## It's now time to have fun!

Please test a number of possibilities.


