---
layout: post
title: Statically-typed R
description: An experiment
date: 13.07.2019
---

Recently, I've been thinking about providing more type safety for R APIs -- below you can find an early attempt to address this. Of course, because of the very nature of R, type checking can be only run-time, and we have to sacrifice features like lazy evaluation (only for typed arguments; other arguments are still lazy), but -- in my opinion -- that's how APIs should be written. All the magic can stay inside, hidden from others' eyes :-)

{% gist e8da655b5d835a725e30a5058cb81baf %}

I struggled a bit with the syntax. The result might not be ideal, but I think it's clear and rather elegant -- any function constructing an object of a certain class (e.g., `character` or `integer`, but also constructors for your own classes) is allowed as type. The binary operator `%:%` is used for defining the output type of a function. For typed arguments, argument name must be prefixed with the type (which is dropped during runtime), as can be seen below:

~~~ R
int_mult = integer %:% function(integer..x, integer..y = 1L) { x * y }
int_mult(2L, 3L) # [1] 6
int_mult(2, 3) # ERROR: is(arg, types[[arg_name]]) is not TRUE
~~~

You can mix typed and untyped arguments in a single definition:

~~~ R
my_fun = character %:% function(character..string, integer..times, opt) {
  if (is.list(opt)) {
    rep(string, times)
  } else {
    NA_character_
  }
}
my_fun(string = "a", times = 2L, opt = list()) # [1] "a" "a"
my_fun("b", 3L, opt = -1) # [1] NA
~~~
