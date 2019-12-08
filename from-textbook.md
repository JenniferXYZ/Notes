# From Textbook

## Definitions

### General-purpose language:

A language designed to be used for writing software in the widest variety of application domains. 

C++, Go, Java, Python, Scheme, Prolog, and Ocaml are all general purpose language. 

### First-class citizens

A **first-class citizen** \(also **type**, **object**, **entity**, or **value**\) in a given [programming language](https://en.wikipedia.org/wiki/Programming_language) is an entity which supports all the operations generally available to other entities. These operations typically include being passed as an argument, returned from a function, modified, and assigned to a variable.

* 1. All items can be the actual parameters of functions
* 2. All items can be returned as results of functions
* 3. All items can be the subject of assignment statements
* 4. All items can be tested for equality

Contrast: In some languages, composite data values such as **arrays** are either statically allocated and never deallocated, allocated on entry to a block of code and unconditionally deallocated on exit from the block, or explicitly allocated and deallocated by the programmer.

### Static Scoping \(lexically scoping\)

sets the scope \(range of functionality\) of a [variable](https://whatis.techtarget.com/definition/variable) so that it may only be called \(referenced\) from within the block of code in which it is defined. The scope is determined when the code is compiled. A variable declared in this fashion is sometimes called a private variable.

C++, Java, Scheme, Python, Ocaml, Prolog

### Dynamic Scoping

creates variables that can be called from outside the block of code in which they are defined. A variable declared in this fashion is sometimes called a public variable.

## Scheme

### Highly Portable

highly portable across versions of the same Scheme implementation on different machines, _**because machine dependencies are almost completely hidden from the programmer.**_

also portable through a set of standard libraries and a standard mechanism for designing a new portable libraries and top-level programs. 

### All objects are first-class objects.

### Call by value language

BUT for st least mutable objects \(objects that can be modified\), the values are **POINTERS** to the actual storage. 

The storage of an object **is not copied** when an object is passed to or returned from a procedure.











