---
layout: post
title: Unusual application of eval()
description: The heritage of Lisp
---

Today I came across a problem when writing a Shiny application: I wanted to dynamically create download handlers, each one with a content function based on the input data. It seemed easy at first:

~~~ R
for (handlerData in allHandlers) {
  output[[paste0("handler_", handlerData)]] = downloadHandler(
    filename = paste0("something", handlerData),
    content = function(file) {
      someFunction(param = handlerData)
    }
  )
}
~~~

But something wasn't right. I got a bunch of identical handlers. A short investigation and it became clear to me that I'd violated one of the essential rules of R.

Now what?

The great heritage of Lisp came to my rescue. I couldn't use variable's value in an ad-hoc function definition... but I could paste it into a character string holding the definition of that function!

~~~ R
for (handlerData in allHandlers) {
  functionString = sprintf(
    'function(file) { someFunction(param = "%s") }', handlerData
  )
  downloadHandlerParams = list(
    filename = paste0("something", handlerData),
    content = eval(parse(text = functionString))
  )
  output[[paste0("handler_", handlerData)]] = do.call(
    "downloadHandler", downloadHandlerParams
  )
}
~~~

[UPDATE]

The above solution is inelegant as crap; here's a better one:

~~~ R
for (handlerData in allHandlers) {
  handlerFunction = substitute(
    function(file) { someFunction(param = handlerParam) },
	alist(handlerParam = handlerData)
  )
  downloadHandlerParams = list(
    filename = paste0("something", handlerData),
    content = eval(handlerFunction)
  )
  output[[paste0("handler_", handlerData)]] = do.call(
    "downloadHandler", downloadHandlerParams
  )
}
~~~

