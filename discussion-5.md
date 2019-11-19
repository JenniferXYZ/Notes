---
description: 11/08/2019
---

# Discussion 5

## Lisp

* Data includes program
* macro vs function
  * macro: quote, if, define, lambda, cond, let/ let \*/ letrec
  * function: +, quotient, cons, car, cdr, list 

### List

'\(1 2 3\)

Lists end with a null. \(\).

* get head: car
* get tail: cdr
* construct a list: cons
* check if empty: empty?
* 
```text
empty list '()
'(1 2 3) 
# we put a quote so the program won't execute (1 2)

(car '(1 2))

(cdr '(1 2))
# returns '(2)

#proper lists
(cons 2 '( 1 2 3))
'(2 1 2 3)
(cons 1(cons 2(cons 3 '())))
'(1 2 3)
(cons 1(cons 2(cons 3 null)))
'(1 2 3)

#IMPROPER list
(cons 2 1)
(2 . 1)
```

### Function

* use define 
* and \(macro\) returns immediately if it evaluates a false

```text
(define a (+ 2 3))
(define (add x y) (+ x y))
add
(add 2 3)

(lambda (x) (+ x 1))
(lambda (x) (+ x 1) 2)
3

(define add (lambda (x y) (+ x y)))
(add 2 3)
5

(define (digit-cnt x)
    (cond [(< x 10) 1]
          ((< x 100) 2)
          ((< x 1000) 3)
          (#t 4)))
(digit-cnt 9)
1

(define (swap x y))
      (let ([y x]
            [x y])
         (list x y)))
(swap 3 2)
'(2 3)

(define (no-swap x y))
      (let* ([y x]
            [x y])
         (list x y)))
(no-swap 2 3)
'(2 2)

(lambda (if) (if 1 2 3))
#<procedure>
((lambda (if) (if 1 2 3)) (lambda (a b c) (+a b c)))
6
((lambda (if) (if 1 2 3)) +)
6

(eq? 6 6)
#t

(eq? '(1 2 3) '(1 2 3))
#f
(equal? '(1 2 3) '(1 2 3))
#t

(and (> 2 1) (> 1 2))
#f
(and 3 (display "here"))
here
(or 3 (display "here"))
3
(and #f (display "here"))
#f

(eval '(2 3))
5

```

### Boolean

* represented as \#t and \#f
* anything other than \#f evaluates to true

### Definitions

* \(define &lt;id&gt; &lt;expr&gt;\)
  * defines a variable 
  * defines a function that returns an expression

    ```text
    (define PI 3.14)
    (define two (+ 1 1))
    ```
* \(define \(&lt;id&gt; &lt;id&gt;\*\) &lt;expr&gt;+\)
  * defines a function with 0 or more arguments
  * first &lt;id&gt; is the function name
  * &lt;expr&gt; defines the body of the function
  * function returns the result of last &lt;expr&gt;

    ```text
    (define (mult_xy x y) (* x y))
    (mult_xy 2 2)
    ```

### Equality

* =
  * tests the equivalency of two numbers
* equal?
  * checks if two arguments have the **the same value**
  * tests **structural equivalence** of two items \(lists, vectors, etc.\)
* eq?

  * tests whether two items **refer to the same thing in memory**
  * **pointer equality**

  ```text
  (= 2 5)
  #f
  (equal? (list '+ '1 '2) '(+ 1 2))
  #t
  (equal? (list + '1 '2) '(+ 1 2))
  #f
  (eq? '(1 2) '(1 2))
  #f
  (define x 10)
  (eq? x x)
  #t
  ```

### Conditionals

#### if

```text
(if test-expr then expr else-expr)
```

* each branch contains a single expression
  * use begin to execute more than one expression

    ```text
    >(if #t
     (begin (display "44") 2)
     4)
    44 2
    ```

#### cond

```text
(cond cond-clause ...)
cond-clause = [test-expr then-body ...*]
             |[else then-body ...*]
             |[test-expr => proc-expr]
             |[test-expr]
```

#### or

* if it produces a value other than \#f, that result is the result of the or expression
* executes every instruction until it has evaluated an expression
* returns the last thing evaluated. If no exprs provided, \#f

  ```text
  >(or (= 1 2) (+1 2) (-4 1))
  3
  >(or #f #t 2)
  #t
  ```

#### and

* if it produces \#f, the result of the and expression is \#f
* keeps evaluating all the expressions till all are \#t. If no exprs provided, \#t
* returns the last thing evaluated

  ```text
  >(and (if (=1 1) "wow" #t) (= 1 1) "great" #t)
  #t
  >(and (if (= 1 1) (display "wow") #f) (=1 1) #t
   "cool")
  wow"cool"
  ```

### let and scoping

* let is used to create local bindings
  * only available in the body of let but not in the clauses
* scope: scheme is lexically scoped

### quote

* e.x. want to use + as a symbol than a procedure
* treats expression as a data

  ```text
  >(+ 1 2)
  3
  >'(+ 1 2)
  '(+ 1 2)
  ```

### eval

* negates quote
* takes a representation of an expression or definition \(as a "quoted" form\) and evaluates it.
* takes a list and treat it like a program

  ```text
  (define (eval-formula formula)
      (eval '(let ([x 2]
                   [y 3])
                 ,formula)))
  (eval-formula '(+ x y))
  5
  ```

### 

