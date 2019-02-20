---
layout: post
title: Range matching
description: More elegant than what people do...
date: 20.02.2019
---

I came up with this idea watching an awful, complicated multiple-if block that assigned different outcomes to several ranges. I thought that something like `switch()` would be more elegant, concise and easier to read. How about this:

~~~ R
x = 7
range_if(
  x,
  .. < 0   ~ "negative",
  .. == 0  ~ "zero",
  .. < 10  ~ "positive but below 10",
  .. <= 20 ~ "between 10 and 20",
  default  = "above 20"
)

# [1] "positive but below 10"
~~~

Those double dots (`..`) represent the tested expression (here: `x`).
(A single dot would look better, but I wanted to keep it compatible with tidyverse.)

{% gist 6dddde8ccc465933784c2e4ee25dd831 %}

PS. Obviously the applications of this function are not limited to matching ranges. You can use any conditions that yield a logical value.
