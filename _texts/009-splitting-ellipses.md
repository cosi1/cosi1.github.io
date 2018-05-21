---
layout: post
title: Splitting ellipses
description: Connecting the dots
---

Have you ever written a function that takes an ellipsis (`...`) as input and passes it further to another function? Sure you have. Now what if there are two functions, both expecting different sets of arguments? Simply passing your ellipsis to both of them will make R complain about unused arguments.

This very short snippet serves as a dispatching mechanism for all functions that you pass the ellipsis to:

~~~ R
runWithEllipsis = function(fun, ...) {
  elli = list(...)
  whichArgs = intersect(names(elli), formalArgs(fun))
  do.call(fun, elli[whichArgs])
}
~~~

Now, simply pass the function and your ellipsis to `runWithEllipsis()`. You can even mix the ellipsis with regular parameters (but remember to explicitly name them):

~~~ R
mySum = function(x, y) { x + y }

myProduct = function(a, b) { a * b }

main = function(x, a, ...) {
  print(runWithEllipsis(mySum, x = x, ...))
  print(runWithEllipsis(myProduct, a = a, ...))
}

main(x = 1, y = 2, a = 3, b = 4, someUnusedArg = 5)

# [1] 3
# [1] 12
~~~

My implementation is extremely primitive (it always evaluates arguments before executing the function and poorly handles some edge cases), but for most uses it's just fine.
