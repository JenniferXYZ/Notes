---
description: 12/04/2019
---

# Lecture Last

## Errors \(Engineering\)

How the programming languages deal with bugs.

### Ways to deal with errors

* Classic Approach: undefined behavior
  * E.x. INT\_MAX+1 in C/C++
  * Gives compiler license to optimize

    ```c
    for (int i=0; i<n; i++)
    //=>
    if (m<n)
    //=>
    for(i=m-n; i--!=0;) //faster that doesn't
                    //work in all cases
    ```
* Signal, exit program
* Throw an exception \(**run-time check**\)
  * C++/Java/Python

    ```text
    try {

        // code that can throw exceptions
        // code to be simple, clear and 
        // optimistic

    } catch (E1 e1){
        // blah
    } catch (E2 e2){
        // blah
    } finally {
        // blah
    }

    // thrower can be in some other class
    ```

  * Java checks exceptions, every method that can generate an exception must be declared thay way
  * 
* **Static Checking**
  * does not need to worry about if program will success on some cases and fail on others
  * E.x. Ocaml null pointers
    * int option
    * wish Ocaml would have subscript errors check at compile time \(harder\) \(a\[i\]\)
* Preconditions
  * E.x. sqrt\(n\) =&gt; pre: n&gt;=0
  * caller must observe preconditions, and callee call assume preconditions.
  * let the programmers to specify the errors. 
* Total definition
  * E.x. x/y
  * define the total functions instead of partial definitions. For example, in division, 1/0 won't raise error, but give special value \(NaN, Inf\). 
  * usually used in IEEE floating

    ```text
    push(u,s)
    pop(s) 
    |
    -----> In partial definition, it is an error
            because stack could be empty
           In total definition, it could give a
            special value when poping an empty
            stack
    ```

## Performance \(Engineering\)

### Cost Models

* Big O Notations, scalability
* Constant factor also matters
* What costs are there
  * **CPU time**
  * **RAM size**
  * Network Throughput
  * Power/Energy

### Cost of a list

| Language | Length/Method | CPU Cost |
| :--- | :--- | :--- |
| Lisp/Scheme | Length L / access \(structure as a linked list\) | O\(\|L\|\) |
| Python | Length L / access | O\(1\) |
| Lisp/Scheme | Length L/ append.l\(M\)  | O\(\|L\|\) |
| Python | if array doesn't fill up/ l.append\(x\) | O\(1\) |
|  | if array fills up | O\(\|L\|\) worst-case |

### Cost of unification/equality operation

Prolog X=Y: 

* Cost depends on which tree is smaller O\(min{ \|X\| , \|Y\| }\), compare and binding
* unification without comparing loops
  * unify\_with\_occurs\_check\(X,Y\)
  * O\(max{ \|X\|, \|Y\| }\)
  * when trying to go into loop, rejected

Scheme

| Method | CPU Time |
| :--- | :--- |
| \(eq? x y\) | O\(1\) |
| \(eqv? x y\) | O\(min{\|X\|,\|Y\|}\) |
| \(equal? x y\) | infinity |
| \(= x y\) | O\(min{\|X\|,\|Y\|}\) |

## Semantics \(Theory\)

Hard part of computer science. Deals with what a program means.

### Some History

1. 1950s: writes semantics of the programming \(e.x. Fortran IBM reference manual\) in English.
   1. Problem: ambiguity + contradictions too common
2. 1960: operational or imperative semantics \(meanings by command\)
   1. To define a language L, write a program in a known language M that interprets programs in language L, then run interpreter on your L-program
   2. e.x. Lisp: defined via an interpreter written in Lisp 
3. ~1970: axiomatic semantics \(meanings via logic\)
4. ~1975: denotational semantics \(meanings via functions\)

{% hint style="info" %}
1&2 define ML subset of Prolog
{% endhint %}

```text
m(E, Env, V)

Example 1
let X=E in F, let (X,E,F)
m(let(X,E,F), Env, V) :-
    m(E, Env, EV),
    m(F, [X=EV|Env], V).

Example 2
fun X->E, fun(X,E)
m(fun(X,E), Env, fun(X,E)).

f X, call(f,X)
m(call(F,E), Env, V):- //dynamic scoping
    m(F, Env, fun(X,FE)),
    m(E, Env, EV),
    m(FE, [X=EV|Env], V).
```

### Static Semantics

rules of the language you can find out before it runs

### Dynamic Semantics

these things are obvious to programmers but you have to nail down all the details

* Operational semantics
  * If you want to say what a program means when you run it, you explain it by writing an interpreter for it
* Axiomatic semantics
  * Explain p in a language L by providing general axioms and rules of inference about L and then derive a conclusion from it
  * **Supply axioms and rules of inference!**
  * **More abstract approach, but to some extent, more satisfying approach**
* Denotational semantics

  * Supply a function from program to meanings
  * **Typically, these meaning are functions**
  * If you have a program P, and you want to know what it means, call "meaning P"

