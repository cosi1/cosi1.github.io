---
layout: post
title: User-friendly paste0()
description: Concatenate strings with an infix operator
---

~~~ R
`%+%` = paste0
~~~

Now you can concatenate strings like in many other languages:

~~~ R
cat("Result: " %+% x %+% "\n")
~~~

