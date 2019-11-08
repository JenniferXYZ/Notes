---
description: 10/21/2019
---

# Lecture 7

Software evaluation \(types\) \| Language evaluation -&gt; successful language evolve 

## CPU Evolution: 

BASIC \(interactive\) developed for GE-225 \($1 million\) \(1962\)

* takes 40 μs to add
* 500 μs to divide
* ~40kB RAM
* 20 users simultaneous use
* to solve small memory: use short identifiers for string identifiers

PDP-11

* 4 μs to add
* ~16kB RAM
* 1.2 μs memory cycle time \(load & save is relatively faster 3 times than adding\) 
* \*p + 27

C Programming Language

* Unix =&gt; Linux

Today's CPU

* 1 ns to add
* 100 ns to load from memory
* Java doesn't have pointers. Pointers \(\*p\) works well in PC in the past. 

## Java \(1990's\)

More like BASIC

Design goals:

* "write once, run everywhere"
* short \(16-bit\), int \(32-bit\), long\(64-bit\) on all machines
* Interpreter model for implementation

  ```text
  Foo.java    -> java c    -> Foo.class    -> Java
                  |                |            |
          witten in Java ->   byte codes   -> witten in C/ASCII
                  |                
             stack machine -> JVM
  ```

* Java is running C / ASM \(abstract state machine\) is an executable C code
* Java takes byte codes and add it to code and run
* More reliable than the disasters of C++
  * Automatic array bounds checking and the lack of manual memory management \(e.g. no pointers in Java\) make certain classes of programming mistakes that often cause serious security holes \(such as buffer overruns\) impossible. Most other modern languages share this feature, but C and C++, which were dominant \(and still are major\) application development languages at the time Java first appeared, do not.
* Each machine has different java interpreter. But Foo class can be transferred in different PC, JVM is same everywhere
  * compilers: translate from source to machine code \(runs on machine\)
    * Pros: run-time and performance 
  * interpreter: transform source to _high level_ intermediate form 
    * high level: interpreter runs this directory written in machine code
    * Pros: portability + safety + debuggability 
      * debuggability: sometimes it is possible for 2 operators in C have same expression in machine code, which is hard to identify with interpreter. It's easier to identify 2 operators

### Just-in-time \(JIT\) Compiling

Hot spot compiling: interpret the program while profiling it \(\# of times the instructor is executed\)

* reads byte code as its source, and convert to machine code.
* table indexed by byte code offsets
* compile mostly often used chunks to machine code
* improves efficiency







  

### Dynamic Linking









v.s. self-modifying code \(e.g. C\):

* Definition:   code that alters its own instructions while it is executing – usually to reduce the instruction path length and improve performance or simply to reduce otherwise repetitively similar code, thus simplifying maintenance. Self-modification is an alternative to the method of "flag setting" and conditional program branching, used primarily to reduce the number of times a condition needs to be tested. 
* security issue
* hard to debug
* bug prone 

### Type

#### Definition: 

set of values \(int etc.\) + set of operations \(+ / - & \* etc.\)

| Primitive Types | Constructed Types |
| :--- | :--- |
| int, bool, float |  Bool \[ \]; struct {char c; float f;} |

#### Portability issues of type: 

"float" - IEEE-754 32-bit

#### Uses of types:

* Annotations \(C++, java like\)

  * useful for reader of code 
  * useful for compiler of code =&gt; **more efficient** 

  ```text
  int x = f(z); (x->%edi)
  ```

* Inference: \(Ocaml likes this\)

  ```text
  a     +     b      *     c
  |           |            | 
  float      int          char
    |          |____________|
    |_______________int 
          float
        
  ======================================
  let rec rev (x: 'a list)
  ```

* Type checking \(redundancy to catch dumb mistakes\)

  ```text
  char *p = a + b
            int_int
              int
  ```

#### Dispute: static vs dynamic type checking 

* static: checks at compile time, eliminate type error from running code \(**reliability**\) \(e.x. Java, C/C++\)
* dynamic: checks at run time \( you as a programmer can write a little quicker because you do not have to specify types every time \(unless using a statically-typed language with _type inference_\).\), **flexibility** \(e.x. Python\) 

#### Strongly typed

Cannot subvert the type system

#### Abstract v.s. Exposed Types: 

* Abstract: only operations are visible, you cannot examine representation
* Exposed: implementation is visible
  * e.x. typedof struct {double re, im} cplx
  * **Cons: messy**
  * **Pros: let the programmer take adv of underline representation**

#### **Float x86-64 32-bit IEEE FP**

```text
 -----------------------------------------------
 |  s  |     e      |             f            |
 -----------------------------------------------
  sign    exponent            fraction
```

$$
\pm 2^{e-127}*1.f_2
$$

$$
0<e<255, f=0 \rightarrow   \pm 2^{-126}
$$

$$
e=255, f=0 \rightarrow   \pm \infty
$$

$$
e=255, f=0 \rightarrow   \pm NaN (23-bit)
$$

\(a - b != 0\) == \(a == b\)

#### Subtype

* If class A is a subclass of type B, it is a **subtype**.
* A = b should be allowed if B’s type is a subtype of A’s type. ○ Equivalent to tryna to determine if int subset of long \(b subset of a\)
* The idea is that in order for something to be a subtype s of another type t, s has to be able to do all the operations that t can do.



