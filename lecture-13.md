# Lecture 13

## Scheme continued

### Why no while/for loops in scheme

Such constructs are unnecessary; iteration in Scheme is expressed more clearly and succinctly via recursion. Recursion is more general and eliminates the need for the variable assignments required by many other languages' iteration constructs, resulting in code that is more reliable and easier to follow. Some recursion is essentially iteration and executes as such.

### What is the point of let instead of lambda? 

Both of them bind local variables.

When you write the code using a let, it runs in the order that you call them. Look at the order of evaluation does matter because arguments to a function have to be evaluated in Scheme before the function body is evaluated. 





