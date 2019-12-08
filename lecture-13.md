# Lecture 13

## Scheme continued

### Why no while/for loops in scheme

Such constructs are unnecessary; iteration in Scheme is expressed more clearly and succinctly via recursion. Recursion is more general and eliminates the need for the variable assignments required by many other languages' iteration constructs, resulting in code that is more reliable and easier to follow. Some recursion is essentially iteration and executes as such.

### What is the point of let instead of lambda? 

Both of them bind local variables.

When you write the code using a let, it runs in the order that you call them. Look at the order of evaluation does matter because arguments to a function have to be evaluated in Scheme before the function body is evaluated. 

### Equality operators

#### eq? 

* pointer comparison. \#t iff its arguments refer to the same objects in memory
* if two arguments are eq, they are also eqv and equal 

#### eqv?

* like eq? when comparing objects, but also comparing numbers
* returns \#t iff arguments are eq **OR** if its arguments are numbers of the same value. It does not convert integers to floats when comparing integers and floats though.

#### equal?

* returns \#t if the arguments have the same structure
* equality comparison
* slower because it is a recursive comparison
* does NOT just follow a list to its end, but it also recurses down through two sublists

#### =

* numerical comparison 

### What are some of the disadvantages of continuation approach versus POSIX threads?

1. We don't get processor improvement because there is only one thread active in any given time
2. Only one instruction pointer that is actually running
3. Won't suffice if you want to build a true multi-threaded system
4. saves energy tho
5. Available in other languages but perhaps NOT quite as elegantly as this 

### Do we have something similar to continuation in C/C++?

No. We cannot use lambdas in C/C++.

* This procedure is something we will hand off for someone else to run
* you cannot have a procedure that is active after we have returned.
* This makes continuations not work in C/C++, but **works well in Scheme**

### Do we have something similar to continuation in python?

Take a snapshot of where your function is and resume that snapshot later.

This is a central problem in **Twisted** framework

Deferred object in **Twisted**

## Meta-programming

 **Metaprogramming** is a programming technique in which computer programs have the ability to treat other programs as their data. It means that a program can be designed to read, generate, analyze or transform other programs, and even modify itself while running.

* **Macros** and metaprogramming is controversial
* Debugging tools go haywire because they are NOT on the same level
* Milstein loves meta programming and goes way off the deep end
* Eggert is far more skeptical because we might be getting into trouble

Macros are troublesome, and this is part of meta-programming that kind of does not work well. 

* Macros might have side-effects
* Macros could possibly be slow and expensive
* Might cause the problem of capture
  * Suppose we have a macro implementation in our code. And we are dealing with a variable "v".
  * In this case, macro "v" can collide with variable "v".

**How to solve this problem in C**

Tell the pre-processor to give me a symbol that the program isn’t using. 





