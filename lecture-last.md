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

## Semantics \(Theory\)

## History of Programming Languages

