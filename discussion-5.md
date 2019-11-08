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

* get head: car
* get tail: cdr

```text
empty list '()
'(1 2 3) 
# we put a quote so the program won't execute (1 2)

(car '(1 2))

(cdr '(1 2))
# returns '(2)
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



