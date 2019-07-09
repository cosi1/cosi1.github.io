---
layout: post
title: Plus-equals
description: Unbelievable
date: 21.09.2016
---

Found this [on Twitter](https://twitter.com/henrikbengtsson/status/774434384610938880).

This hack works for other operators as well, like `+<-`, `-<-` and even `!<-`. This made me come up with an idea of two Python-like operators for increasing/decreasing scalars/concatenating vectors:

~~~ R
`+<-` = function(x, value) {
  if (length(x) > 1) c(x, value) else x + value
}

`-<-` = function(x, value) {
  if (length(x) > 1) x[x != value] else x - value
}

# Some examples:
x = 5
+x = 7
print(x) # [1] 12
-x = 15
print(x) # [1] -3

y = c(1, 3, 5)
+y = 7
print(y) # [1] 1 3 5 7
-y = 1
print(y) # [1] 3 5 7
~~~

They are not really reliable (you need to know the length of the input variable before the operation or else the result may be a surprise to you), but it's amusing, isn't it?


[UPDATE]

This is even more impressive:

~~~ R
# A logical function
even = function(x) { x %% 2 == 0 }

`%is%<-` = function(x, fun, value) {
  ifelse(fun(x), value, x)
}

x = 1:10
x %is% even = NA
print(x) # [1]  1 NA  3 NA  5 NA  7 NA  9 NA
~~~

(Inspired by [this article](http://karolis.koncevicius.lt/posts/r/little_known_features/little_known_features.html))

