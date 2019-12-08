# Some example codes

## Scheme

_**memv**_ takes two arguments, an object and a list. It returns the first sublist, or tail, of the list whose car is equal to the object, or \#f if the object is not found in the list. The value of memv may be used as a list or as a truth value in a conditional expression.

```text
(define memv
  (lambda (x ls)
    (cond
      [(null? ls) #f]
      [(eqv? (car ls) x) ls]
      [else (memv x (cdr ls))])))

(memv 'a '(a b b d)) => (a b b d)
(memv 'b '(a b b d)) => (b b d)
(memv 'c '(a b b d)) => #f
(memv 'd '(a b b d)) => (d)
(if (memv 'b '(a b b d))
    "yes"
    "no") => "yes"
```

_**remv**_ defined below takes two arguments, an object and a list. It returns a new list with all occurrences of the object removed from the list.

```text
(define remv
  (lambda (x ls)
    (cond
      [(null? ls) '()]
      [(eqv? (car ls) x) (remv x (cdr ls))]
      [else (cons (car ls) (remv x (cdr ls)))])))

(remv 'a '(a b b d)) => (b b d)
(remv 'b '(a b b d)) => (a d)
(remv 'c '(a b b d)) => (a b b d)
(remv 'd '(a b b d)) => (a b b)
```

The following two definitions of _**factorial**_ use named let expressions to compute the factorial, n!, of a nonnegative integer n. The first employs the recursive definition n! = n × \(n - 1\)!, where 0! is defined to be 1.

```text
(define factorial
  (lambda (n)
    (let fact ([i n])
      (if (= i 0)
          1
          (* i (fact (- i 1)))))))
```

The second is an iterative version that employs the iterative definition n! = n × \(n - 1\) × \(n - 2\) × ... × 1, using an accumulator, a, to hold the intermediate products.

```text
(define factorial
  (lambda (n)
    (let fact ([i n] [a 1])
      (if (= i 0)
          a
          (fact (- i 1) (* a i))))))
```

