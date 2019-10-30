---
description: 10/16/2019
---

# Lecture 6

1. functional programming
2. type inference

## Compiler and Interpreter

### Compiler

* Compiler will take your program and translate it into machine code \(low level code that has the same effect as that high level instruction\)

### Interpreter

* An interpreter keeps source code in RAM, execute it directly
* Pros:
  * portable, since you can run the same instructions as whatever machine you’re using
  * simple to write and read
  * better with cross platform programs
* Cons:
  * slower, because it does error checking and catches errors as they happen \(e.g. index checking\)

How to get both the high performance of compilers with the bug catching features of an interpreter?

* Use interpreter while developing and use compiler for production but there is a problem between if the two will output the same results for the same program.

## Three types of programming languages

### Imperative \(Procedural\)

Follow commands and sequence them C1; C2; … And also use variables and make assignments.

### Functional

Functions are the unit and you hook stuff together using function calls f\(x\) and you **don’t use any assignment statements**. **Never change the value of the variable**. Variables never vary in a functional language.

### Logic

Predicates are the units of computation. They are statements that are true or false. The syntax is p if q. **No assignments and no function calls.**

## Ocaml

### Properties

* It has static type checking to make sure that you’re not calling functions with the wrong types =&gt; code more reliable
  * It's like C++ and Java but not Python and Javascript
* Has type inference =&gt; You don’t have to write the types down in Ocaml
  * This is like Python and Javascript but unlike C++ and Java.
* has a garbage collector
  * This is like Python and Java and Javascript, but unlike C and C++ cuz you gotta deal with your own memory
  * Typically though, the automatic one will have worse performance than a manual collector given that that programmer knows how to use it
* Good support for higher order functions
  * This is like Python a little, but unlike everything else.

```ocaml
if 1<2 then "a" else "b";;
-: string = "a"

if "a" then 1 else 2;;

if 1<2 then "a" else 37;;
```

```ocaml
let p = (1,2);;
-: p:int*int=(1,2)

let q = 1, "abc", false;;
-: a:int*string*bool = 1, "abc", false

let int = ();;
-: int:unit=()
```

### Tuples

* pros: heterogeneous \(can be of diff type\) \(more flexible\)
* cons: size is known \(fixed\)

```ocaml
let id x=x
let id = fun x -> x (*it can't look into the argm,
                because identity function is supposed
                to take any types*)
let cp = fun x -> (x,x)

```

```ocaml
let r = (3,5,r);;
(*r is not declared yet, so cannot create a recursive
tuple*)
let head = fun x->fst x;;
(*<=> let head = fst;;*)

```

### Lists

* pros: homogeneous
* cons: size is unknown \(part of type\)

```ocaml
[1;"a"];;
(*you CANNOT do this to ocaml ugh*)
[1;-3;2+8];;
-: int list=[1;-3;10] (*this is okay*)
[];;
-: 'a list=[] (*'a: generic type*)
[3;5] = [];;
-: int list = 'a list
[] = ["abc"; "abf"];;
-: 'a list = string list
[[]; [3;4]; []];;
-: 'a list; int list; 'b list (*it works when 
                                'a = 'b = int*)
[([]; ["a"]); ([3]; [])];;
-: 'a list * string list; int list * 'b list
-: (int list * string list) list (*this works only
                                when 'a = int
                                'b = string*)
                                
let rec minlist = function 
  | [] -> 99 
  | h::t -> let m = minlist t in if h < m then h
                                else m
-: int list -> int

Let rec minlista inf lt = function
  | [] -> inf 
  | h::t -> let m = minlista inf lt t in 
        if lt h m then h else m
:- 'a -> ('a -> 'a -> boolean) -> 'a list -> 'a = <fun>
```

### Aside on generic implementation

* every object is a x86-64 bit int pointer quantity; typically a pointer

## Functional Programming

```text
(cons x y)
(*construct: create a pointer to pair |x|y| *)
```

```ocaml
let cons(x,y) = x::y;;
-: cons: 'a*'a list -> 'a list = <fun>
let ccons x y = x::y;;
-: ccons: 'a -> 'a list -> 'a list = <fun>
(*ccons is curried cons, for example: *)
let prep1 = ccons 1;;
-:         int list -> int list
prep1 [-5;7];;
-: [1; -5; 7]
(*compare to non-curries cons*)
let rep1 = 
  l = cons(1,l);;
let ccons = (::);; (*the same as L3*)

(*reverse currying*)
let rccons y x = x::y;;
-: 'a list -> 'a -> 'a list (*not recommended*)

```

**currying**: \(each function takes exactly one argument\)

```ocaml
(+);; (*when you have parentheses around +, it refers
        to a function*)
-: int -> int -> int -> <fun>

let add1 = (+) 1;;
add1 15;;
-: int = 16
```

```text
p = (cons c y)
(car p) => x
(cdr p) => y
cons (x,y)
ccons x y
```

```ocaml
let car x::_ = x;;
-: car 'a list -> 'a = <fun>
(*we will get a compile-time warning, because 
this is not exhaustive*)

let car = fun l -> match l with
                     | x::_ -> x;;
(*This is a partial function, what if we pass an 
empty list*)
car [];;
(*this causes a runtime-error*)                     
(*====================to fix it===================*)
let car1 = (function 
  | x::_ -> x
  | [] -> []);; (*function expr = match function*)
-: car1: 'a list list -> list (*this only works
                              for a list of lists*)

let gcar d l = match l with
                | x::_ -> x
                | [] -> d;;
(*or*)
let gcar d = (function 
  | x::_ -> x
  | [] -> d);;
-: gcar: 'a -> 'a list -> 'a = <fun>
(*d is the msg we return when empty list is passed
 this way, gcar works on any kinds of lists.*)
 let icar = gcar 0;; (*we curry gcar function*)
 -: int list -> int
 
```

## Recursion

```ocaml
let rec rev0 = function
    | [] -> []
    | h::t -> (rev0 t)@h;;
-: rev0: 'a list list -> a list = <fun>
(*Using type to debug*)
rev0 [[3;4];[-9;2;1];[7]];;
[7;-9;2;1;3;4] (*rev0 function reverses and flattens
the list at the same time*)
===============one fix=====================
let rec rev1 = function
    | [] -> []
    | h::t -> (rev1 t)@[h];;
rev1 [[3;4];[-9;2;1];[7]];;
[[7];[-9;2;1];[3;4]] (*kinda fixed the problem, but
                        SLOW. O(N^2) (@ is O(N)*)
==============final fix======================
(*reverse and append (revapp a r)*)
let rec revapp a = function
    | [] -> a
    | h::t -> revapp (h::a) t 
(*we made O(N^2) to O(N)*)
-: revapp: 'a list -> 'a list -> 'a list
let rev = revapp [];;
        'a list -> 'a list
        
```



