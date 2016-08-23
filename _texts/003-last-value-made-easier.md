---
layout: post
title: .Last.value made easier
description: 8 keystrokes less!
---

If you're like me, you probably use R as a handy calculator. Unlike typical calculators, however, this one doesn't instantly give you access to the result of the last calculation. `.Last.value` is a pain to type (even with autocompletion), but you can define something shorter:

~~~ R
. = function() .Last.value
~~~

From now on, `.()` will yield the last calculated value.

Btw. Isn't it great that R lets you define a function named `.`? :-)

