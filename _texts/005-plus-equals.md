---
layout: post
title: Plus-equals
description: Unbelievable
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
