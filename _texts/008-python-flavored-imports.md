---
layout: post
title: Python-flavored imports
description: Selective imports and aliases
---

Inspired by [this recent blog post](https://trinkerrstuff.wordpress.com/2018/02/22/minimal-explicit-python-style-package-loading-for-r/) found on R-Bloggers, I wrote two very simple functions that tackle the problem in a slightly different way:

{% gist 64a11cc5ba1a680d84b8796d11eec289 %}

Now, you can import selected functions from a package (including unexported ones) to the global namespace without littering it with all functions from that package:

~~~ R
importFrom("shiny", c("hr", "%OR%"))
~~~

or make a more convenient alias for that package's namespace:

~~~ R
importAs("dplyr", "dp")
~~~

