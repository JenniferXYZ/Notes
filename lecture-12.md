---
description: 11/18/2019
---

# Lecture 12

## Scheme

* Teaching subset of Lisp and not exactly a subset \(differs\)
* Lisp has been a very popular AI language
* Traditional AI - NOT machine learning
* Based on logic and arithmetic
* A language that has a long tradition in computer science and ideas that when they were first introduced were considered way too bleeding-edge and inefficient
* Slow, academic side of things
* Too slow for academic use

## Advantages of Scheme

### Scheme is OO in some sense

* Scheme values are **all Objects** in the OO programming sense
* **Have pointers and addresses**
* Dynamically allocated so program can allocate an Object whenever it feels like and calls the equivalent of “new” whenever it wants
* They are never freed, so the program never has to free an object
* Up to the system of when to handle this condition

### Concept of Garbage Collector

* Like M.L., OCaml, Java, Python
* Unlike C++, C

### Types in Scheme:

* Everything is an object in Scheme including integers!
* Objects at runtime have types
* They belong to object values
*  Manifest types are obvious if you read the program, you can just see it!

### Dynamic Checking 

* Do dynamic type checking here, not static type checking.
* Scheme is like Python which does dynamic type checking but unlike OCaml, Java, C, C++ in terms of interpreted side rather than compiled side

### Scope checking

**static scoping**

* Scope checking - we want to do all that checking at compile-time
* Use caller’s names to resolve things you don’t know
* very simple scoping strategy that means you don't know what X means until runtime

{% hint style="info" %}
#### Q. What if you have two variables with the same name?

A. That would be an error in scope.
{% endhint %}

* You look at the closest call and this is like static scoping in C

#### Bash uses dynamic scoping for environment variables

* In CS 35L, we constantly tell you to set the PATH environment variable so you can run a shell script to run the value of that variable
* **Performance issue for scoping \(Scheme doesn’t use this!\)**
* **Advantage of static scoping is speed!**
* **Misspellings in the program are also checked before it runs in static scoping**

{% hint style="info" %}
#### Q. Why would you want dynamic scoping?

A. Lessens the number of arguments at runtime. Like setting the PATH environment  
variable modifies all of your shell scripts. Set your PATH variable to use your version of  
grep.
{% endhint %}

* Gives you extra flexibility and another way to modify the behavior of programs besides the standard ones \(passing in extra arguments\)
* call by value
* Evaluate the argument, get a value, and pass a copy of that value \(a copy of the pointer to an object\) to the called function
* Objects of procedure types are first-class objects
* Same namespace and values as everything else
* All of this is the same to Scheme and we don’t have a special sort of case for procedures

### Continuations

* A special subset of procedures 
* Not functions
* Procedures you create and they immediately represent the entire future of your program which you later replay
* like snapshots but not really snapshots

## Lisp

Metaprograms has made it survive for many years

* **tail-recursive** optimization is required
* call zillions of f until you call h
* Stack size proportional to recursion depth, so you will have problem if you try to concatenate a list of one million
* Depth of the stack is bounded
* 
