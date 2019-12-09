# Lecture 14

## Garbage Collector

## Some final pre-prep questions

### Recursion and tail-recursion

Definition: save the results of the recursive call and you can just append the result of that. You get it over with and never have to come back to that level again.

If a function is tail-recursive, you have to call the function and this is the last thing we do, so we cannot remember what the value is. 

If we want to hold the value, we need an accumulator so we can pass things on to the recursive calls. So we add a parameter to the function call to handle accumulation. 

### An advantage of static type-checking over dynamic type checking, and provide an Ocaml expression that illustrate that point. 

You know something is messed up before you run the program.

e.x. let bob=3, and then you try to do bob@&lt;something&gt;

However, dynamic checking allows for more flexibility. 

## 



