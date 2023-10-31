---
title: "Section 09: ImageShop"
author: Jed Rembold and Eric Roberts
date: "Week of October 30th"
slideNumber: true
theme: monokai
highlightjs-theme: monokai
width: 1920
height: 1080
transition: fade
css:
  - css/codetrace.css
  - css/roberts.css
---


## Problem 1
:::incremental
- Write a function
  `def create_cumulative_histogram(hist)`{.mypython .inlinecode}
  that takes a histogram array `hist` and returns a new array in which each value in an index represents the sum of all values in `hist` up to and including that index.
- This new array is called the _cumulative histogram_.
- In solving this problem, you should refer back to the histogram problem you wrote for Problem Set 5 for the definition of the histogram array. In particular, you can use the function `create_histogram_array` to create a histogram array to feed into `create_cumulative_histogram`.
:::

## Example: Cumulative Histogram
- As an example, suppose that you have executed the following lines:
  ```mypython
  SCORES = [ 8, 7, 8, 6, 8, 10, 4, 9, 6, 9, 7, 8 ]
  histogram_array = create_histogram_array(11, SCORES)
  ```
  using `create_histogram_array` as you implemented it for PS5 to create the following histogram array:
  \begin{tikzpicture}%%width=70%
  \foreach[count=\i] \v in {0,0,0,0,1,0,2,2,4,2,1} {
    \node[MBlue, draw, minimum size=1cm, font=\Large, thick, label={[MOrange]below:\i}] at (\i,0) {\v};
    }
  \end{tikzpicture}
- The corresponding cumulative histogram should look then like:
  \begin{tikzpicture}%%width=70%
  \foreach[count=\i] \v in {0,0,0,0,1,1,3,5,9,11,12} {
    \node[MBlue, draw, minimum size=1cm, font=\Large, thick, label={[MOrange]below:\i}] at (\i,0) {\v};
    }
  \end{tikzpicture}
 
## Solution 1: Keeping a Running Total
```{.mypython style='font-size:.8em; max-height: 800px;'}
def create_cumulative_histogram(hist):
    """
    Returns the cumulative histogram corresponding to the histogram
    array hist.  Index k in the cumulative histogram indicates the
    number of values less than or equal to k in the original 
    sample.
    """
    chist = [ 0 for i in range(len(hist)) ]
    total = 0
    for i in range(len(hist)):
        total += hist[i]
        chist[i] = total
    return chist
```

## Solution 2: A Pythonic One-Liner
```{.mypython style='font-size:.72em; max-height:850px;'}
# Implementation notes: create_cumulative_histogram
# -------------------------------------------------
# This implementation of create_cumulative_histogram uses the Python
# features of list comprehension, slicing, and the library sum function
# to reduce the code to a single line.  Each element in the comprehension
# is the sum of all the elements at or below that index.  This version
# performs many more additions than the expanded version because the
# sum is recomputed each time.

def create_cumulative_histogram(hist):
    """
    Returns the cumulative histogram corresponding to the histogram
    array hist.  Index k in the cumulative histogram indicates the
    number of values less than or equal to k in the original sample.
    """
    return [ sum(hist[:i + 1]) for i in range(len(hist)) ]
```
