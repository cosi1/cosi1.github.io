---
layout: post
title: Feature toggles in R
description: Continuous deployment made easy
date: 10.09.2018
---

Recently, a colleague introduced me to the concept of [feature toggles (or switches)](https://en.wikipedia.org/wiki/Feature_toggle). In short, it is a software engineering technique that allows for selective deployment of new features to different environments (development and production) without the need to use separate code bases (e.g., different Git branches).

Thanks to the nature of R, it's easy to implement an elegant mechanism, based on packages. First, we need to implement two one-liners -- this will be the core of our solution:

{% gist 7234dc2bcb00b990dfd4e82c5735537a %}

Now, suppose we have a package with one exported function, named `main()`, located in main.R - it multiplies its input by two (I couldn't come up with a more sophisticated example...):

~~~ R
#' @export
main = function(x) {
  x * 2
}
~~~

We've developed an improved version of this function, which multiplies x by itself. Now we want to crash-test it on the development machine, but without affecting the production environment (where -- according to the rules of continuous delivery/deployment -- the code might land before tests end). Let's put the new version of the function in mainDev.R (but *not* export it!) and add the file to the `Collate` section of DESCRIPTION *before* main.R,

~~~ R
main.new = function(x) {
  x * x
}
~~~

To add a feature switch to `main()`, we'll simply modify one line in main.R:

~~~ R
#' @export
main = toggle(main.new) %||%
function(x) {
  x * 2
}
~~~

Now, in the deployment script (this is the script that installs the package on the machine, typically run by Jenkins or other deployment engine) we have to "tag" the environment by setting a system variable (with `set`, `setenv`, `export`, etc.) -- in this example the variable's name is `env`, and it's set to `dev` in the development environment and `prd` on the production, but of course that's arbitrary.

When the package is built and installed to libraries in both environments, we'll have *two versions* of the same package, built from the same source: `main(5)` will return 10 on PRD, but 25 on DEV.

