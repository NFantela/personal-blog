---
title: "Javascript Currying and Pipes"
date: 2020-09-03T10:11:03+02:00
draft: false
description: Exercise in Functional programming and function chaining.
slug: javascript-currying-and-pipes
tags: ["javascript", "functional-programming"]
---

{{< figure src="/images/javascript-currying-and-pipes.jpg" alt="Javascript Currying and Pipes" >}}

If you have ventured in **RxJS** the concept of `.pipe()` is very fammiliar. Here we will recreate simmilar functionality

### Creating our two main functions

#### Curry 
{{< gist NFantela 683631343ba3ce1e01430fc431707cc1 "curry-function.ts" >}}
Simple enough, we take in Function as argument and return a function. If the arguments length is 
greater than passed Fn arguments length we immediately call it. If not we return a new bound function.

#### Pipe 
{{< gist NFantela 683631343ba3ce1e01430fc431707cc1 "pipe-function.ts" >}}
We take in array of functions and in our case return a function taking in 1 argument.
The passed functions are stored in closure while the X argument will be used to kick of 
`reduce()` call in returned function.

#### Combining the two
{{< gist NFantela 683631343ba3ce1e01430fc431707cc1 "curry-pipe.demo.ts" >}}
First we "store" 2 functions with our `curry()` call that will be later used.
Now we call our **pipe** function passing our 2 curried function calls inside as arguments. At this point
the split() and join() will get their first argument which is *separator*.
Now we can call the result of pipe call and store it in result. This kicks of the `fns.reduce((fnRes, nextFn) => nextFn(fnRes), x);` and passes it its needed X argument which is in our case string *"My Little Pony"*;

### Live Stackblitz demo of Javascript Currying and Pipes.
[Currying and pipes](https://stackblitz.com/edit/pipe-function-recreated)