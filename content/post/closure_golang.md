+++
date = "2016-03-31T15:14:47+05:30"
description = "Detailed account of closures in golang with examples."
title = "Closures in golang"
tags = ["golang", "closure", "go", "anonymous functions"]
+++

A closure is a function that you can pass around that retains the same "environment" as the one it had when it was created.
In other words, the function defined in the closure 'remembers' the environment in which it was created. It takes some time to
get a hang of closures. At least it took me sometime to get going on closures. Hopefully this post will help you understand the same.

Before getting into what `closures` are, lets understand the basics first - functions/ anonymous functions.

#### 1. Anonymous functions
Functions with name are named functions!. Functions which can be created without a name
are anonymous functions. _That was easy :)_. As you can see from code snippet, one can create an anon function and
call directly or one can even pass around anonymous functions. Generally closures make use of
anonymous function, whereas that always need not be the case. In golang, one can create anon functions
and pass functions as arguments to functions. Functions are first class.

`getPrintMessage` creates an anonymous function and returns it. `printfunc` gets the
anon function and calls it.
{{< gist keshavab 279e74a2c9b16fbc90c5db33fce080c1 >}}

#### 2. Closures
The function foo is an inner function and still has access to variable text, which is outside of
foo but belongs to outer function. This function foo is called a **`closure`**. It is said to
_close over_ the variables in the outer scope. In this case it _closes over_ `text` variable.
*`foo`* always holds a reference to the `text` variable.
{{< gist keshavab 8f4195dc68bb3200ef3c3172976bb3aa >}}

#### 3. Returning closures and using outside
In this example we see how we can return the closure and use it outside of the function where
it is declared. _foo_ is a closure which is returned to the main function when _outer_ is called.
The actual execution of _foo_ happens in main when it is invoked using **()**. The code outputs `Modified hello`.
So the _closure_ _foo_ still has a reference to the variable _text_ even though the outer function has exited.
{{<gist keshavab 8a8f95286cc2111aafe5e0cd03015f07 >}}

#### 4. Closures and state
Closures preserve state. What this implies is the the state of variables is contained in a closure
at the time of creation(declaration). What this essentially means is  
- the state(variable references) are **same** per creation of a closure. All closures created together have same state.  
- the state are **different** for different creations of a closure.  
Lets digest it with the below gist. Below is a function counter which accepts a start value and returns
two closures - counter(ctr) and incrementer(incr). This implies per invocation of counter, the state (`start` in this case)
is the same value referenced by both the closures. For another invocation of counter, there would be a different `start`
reference which would be shared by both the closures.

In this case first invocation of counter(100), would generate a closure pair ctr, intr which point to 100.
Second invocation of counter(100) would generate **another** closure pair which point to _different_ 100.
{{<gist keshavab 6657265a36ec1748ee0ea1fe71b7e91f >}}

As you can see from output, Initially both values would be 100.
and when incr() is incremented, ctr1() would be same where as ctr() would be 101.
similarly when incr1() is incremented twice, ctr() would be same as 101, while ctr1() would be 102.
{{< gist keshavab 069a0486aa8861a9920defc4f8d36514 >}}

#### 5. Gotchas
One obvious pitfall is creating closures within a loop.
consider the following snippet.

We are creating 4 closures based on slice and returning a slice of closures.
Each closure does the same - print index and the value at that index.
Main function runs through all closures and calls each of them.
{{< gist keshavab b87b506d548f476855909b4613cdcdd2 >}}

Lets see the output.
{{< gist keshavab 1e9cb6ef77d5f214e1297e57f0179724 >}}

_`Surprising`_ right!. Lets uncover this.
If we go back to closure basics, all the closures created once, have reference to same object.
In this case, all of them point to same i and same arr. When the function is actually called in `main`,
the value of i is 3, and hence all of them point to same `arr[3]` which is `4`. Hence the produced output.


Hopefully this clears some air on closures and helps in understanding reading of code using closures.

Suggested reading - These are two excellent articles i found useful. Though they are presented in Javascript,
the concepts remain the same and are applicable.

- [Mozilla developer network - closures](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures)
- [stackoverflow closure discussion](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work?rq=1)
