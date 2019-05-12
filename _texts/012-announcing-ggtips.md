---
layout: post
title: Announcing ggtips
description: Interactive tooltips for ggplots
date: 12.05.2019
---

Courtesy of [our employer](https://www.roche.com/), my colleagues ([Jakub Jankiewicz](https://jcubic.pl) and Michał Jakubczak) and I have just open-sourced an in-house R package we wrote to replace the tooltip functionality of Plotly (which we had found rather immature and hard to customize).

[ggtips](https://github.com/Roche/ggtips) combines R's Grid, JS-driven manipulation of SVG objects, and reactive renderers from Shiny to produce interactive SVG plots embedded in Shiny's `uiOutput` containers. Additionally, it provides a number of low-level (unexported) functions for manipulating grobs (graphics objects).

A simple demo app shows basic features of ggtips; a Dockerized version is also available (see README).

Project homepage: <https://github.com/Roche/ggtips>
