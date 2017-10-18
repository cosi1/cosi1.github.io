---
layout: post
title: Replacement functions once more
description: R magic
---

Replacement functions are one of the best features of R. They are quite easy to write once you learn how to do it, but have you even wondered how expressions like `names(x)[3:4] = c("A", "B")` work?

Let's write a simple function setting field *i* of an object:

~~~ R
`f<-` = function(x, value) {
  x$i = value
  x
}
~~~

We can test it:

~~~ R
l = list()
f(l) = 1:3 # this works
print(l$i)

## [1] 1 2 3

f(l)[2] = 5 # this doesn't
~~~

Now let's write a "getter" function:

~~~ R
f = function(x) {
  x$i
}

f(l)[2] = 5 # ha, now it works!
print(l$i)

## [1] 1 5 3
~~~

The magic behind it has been explained [here](https://cran.r-project.org/doc/manuals/R-lang.html#Subset-assignment). When a replacement is done for a subset of values, R executes the "getter" counterpart of the replacement function under the hood, replaces the subset using `[<-`, and yields the result to the "setter".

