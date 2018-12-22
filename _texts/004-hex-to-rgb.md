---
layout: post
title: Hex to (PyMOL's) RGB
description: A quick one-liner
date: 13.09.2016
---

I needed to convert a bunch of hex-encoded color codes to a set of `set_color` commands used by [PyMOL](https://www.pymol.org/). Here's how I did it:

{% gist 58caa09a93d2510a99ec3a8c8e0ac97b %}

Now all you need is to load a file with your hex codes, convert it and save to another file:

~~~ R
colors = readLines("hex_colors.txt")
pymol_cmds = hex_to_rgb(colors)
writeLines(pymol_cmds, "set_colors.pml")
~~~

This is a small example, yet it shows the power of the pipe operator (**NOTE:** you need to use the original operator from `magrittr` package; [my version](/texts/001-pipe-operator/) doesn't support dots for parameter placement!).

