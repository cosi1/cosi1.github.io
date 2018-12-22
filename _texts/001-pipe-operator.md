---
layout: post
title: Minimalist pipe operator for R
description: ...in 7 lines of code
date: 18.08.2016
---

This is an extremely simplified version of pipe operator (`%>%`) known from [magrittr](https://github.com/smbache/magrittr) and [dplyr](https://github.com/hadley/dplyr).

{% gist da5c5e8fb256536b8e3a2277d5b3f24d %}

The pipe operator allows you to write complex expressions like this:

~~~ R
table(strsplit(gsub("[^a-z]", "", tolower(string)), ""))
~~~

in a much more intuitive form:

~~~ R
string %>%
  tolower() %>%
  gsub(pattern = "[^a-z]", replacement = "") %>%
  strsplit(split = "") %>%
  table()
~~~

making your code much cleaner and legible.

