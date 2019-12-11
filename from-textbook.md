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

Efficient code for lexical scoping is possible because a compiler can determine before program evaluation the scope of all bindings and the binding to which each identifier reference resolves.

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

### Lexically scoped, block-structured

Block structure and lexical scoping help create programs that are modular, easy to read, easy to maintain, and reliable.

#### let \(can be used in body\)

```text
(let ([id val-expr] ...) body ...+)
(let proc-id ([id init-expr] ...) body ...+)
```

The first form evaluates the val-exprs left-to-right, creates a new location for each id, and places the values into the locations. It then evaluates the bodys, in which the ids are bound. The last body expression is in tail position with respect to the let form. The ids must be distinct according to bound-identifier=?.

 The second form evaluates the init-exprs; the resulting values become arguments in an application of a procedure \(lambda \(id [...](https://docs.racket-lang.org/reference/stx-patterns.html#%28form._%28%28lib._racket%2Fprivate%2Fstxcase-scheme..rkt%29._......%29%29)\) body ...+\), where proc-id is bound within the bodys to the procedure itself.

```text
> (let ([x 5]) x)
5

> (let ([x 5])
    (let ([x 2]
          [y x])
      (list y x)))
'(5 2)
================================
> (let fac ([n 10])
    (if (zero? n)
        1
        (* n (fac (sub1 n)))))
3628800
```

#### let\* \(can be used in latter val-exprs\)

```text
(let* ([id val-expr] ...) body ...+)
```

 Like let, but evaluates the val-exprs one by one, creating a location for each id as soon as the value is available. The ids are bound in the remaining val-exprs as well as the bodys, and the ids need not be distinct; later bindings shadow earlier bindings.

```text
> (let* ([x 1]
         [y (+ x 1)])
    (list y x))
'(2 1)
```

#### letrec \(can be used even before its own val-exprs\)

```text
(letrec ([id val-expr] ...) body ...+)
```

 Like let, including left-to-right evaluation of the val-exprs, but the locations for all ids are created first, all ids are bound in all val-exprs as well as the bodys, and each id is initialized immediately after the corresponding val-expr is evaluated. The ids must be distinct according to bound-identifier=?.

```text
> (letrec ([is-even? (lambda (n)
                       (or (zero? n)
                           (is-odd? (sub1 n))))]
           [is-odd? (lambda (n)
                      (and (not (zero? n))
                           (is-even? (sub1 n))))])
    (is-odd? 11))
#t
```



