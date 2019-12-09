# Lecture 14

## Garbage Collector

## Delegation

Definition: In OO programming, implement the method by calling this method from another class. \(or evaluating a member \(property or method\) of one object \(the receiver\) in the context of another original object \(the sender\).

Implicit delegation is the fundamental method for behavior reuse in prototype-based programming, corresponding to **inheritance in class-based programming**.

* In Java, instead of inheriting something, we could have a member inherit something. Although this is sort of common, you could delegate this method from another class and it could be a straight jacket like Java. 

## Parameter Passing

Call methods.

Calls must be fast and clear. 

* E.X. Ada: language used in aeronautics that makes heavy use of call by result and call by result-value
* E.X. Fortran: cares about performance than everything else, uses call by value, call by reference or any of those as long as performance good. Do not rely on aliasing in Fortran. 

### Call by value

* widely used in **Java, C++ etc**
* Pros: **Simple**
* Cons: 
  * Does not work well with large objects
  * unnecessary crashes if expressions isn't needed
  * It could make your object crash, while other things would be okay
* One way to attack it: call by reference

### Call by reference

* Address get passed instead of a copy of the data
* the callee put a star \(\*\) in front of the argument
* **Compiler with use call-by-reference but they try to make it efficient in the normal case that you don't have aliasing**
* Pros:**Large objects passed efficiently**
* Cons: 
  * Accidental modification
* Solutions to modification
  * const in C++
  * **Aliasing**
    * assume m, n are of type int, it is possible that m and n refer to the same object
    * We want to calls to be fast and clear, but in some cases **aliasing hurts performance**

### Call by result

Execute the function and when it returns, you copy the argument's value back to the call. It decouples local variables from the globals  \(i.e. heap objects\)

* Pros: you don't worry about aliasing between parameter and global variables
* Cons: still have the problem of passing two arguments are the same \(e.x. f\(buf, buf\)\)

### Call by result-value

Combination of call by value and call by result. When it is done, it copies its result back to the caller. 

* Different with call by reference:
  * **the callee is operating with a local copy of the parameter and doesn't have to worry about aliasing**
* Pros:

  * Gets the safety without having the problems of call by reference, and looks like the original call by reference style
  * Gets rid of aliasing by having all parameters be copies of the original, but if you modify the parameters, since they are independent copies, they cannot be aliases of each other
  * When you return, you copy these back to the original and run the original code

### Call by unification \(Prolog\)

### Call by name \(call by reference ::\)

Functions: pointers \(\*n\) callee

If you have a function f, you don't pass n directly. Rather, you use Lisp notation and pass in a func and when you call it, you will return n.

* This is what you pass at the low-level but you haven't evaluated n at all
* packaged up evaluation of n in a procedure that will be called in a callee
* **what is actually generated in the object code is a lambda expression**

\*\*\*\*





