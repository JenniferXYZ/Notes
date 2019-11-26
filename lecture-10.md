---
description: 11/06/2019
---

# Lecture 10

## Reversing a list

### Naive Reverse, benchmark \(O\(N^2\)\)

```text
reverse([],[])
reverse([X|L],[R]):-
    reverse(L,_|)
    append(_|,[X],R)
```

### Accumulation, O\(N\)

```text
revapp(L,A,R)
revapp([],A,A)
revapp([X|L],A,R)
    revapp(L,[X|A],R)
```

## Backtracking 

Backtracking might fall into infinite loop

Be cautious when writing the program.

Here is one example of infinite backtracking:

```text
member(x,[x|_])
member(x,[_|L]):-member(x,L)

?-member(3,L)
L = [3,_27]; (*deny, backtrack*)
    X1=3, L1=[_96|_28]
    member(3,[_96|_28])
    96 = 3
    ... (*it will keep backtracking if you do not
    accept the answer*)

?-member(3,[x,y,z,w]), fail (*member psuedo-ly 
                             bounded, it will only
                             backtrack four times,
                             and then give up*)
                             
```

```text
pick a list P
append(P1,P2,P) ...
If P is of known size, okay
If not, backtracking trouble
```

#### Advantages

* Because these data structures are pushed onto the stack, accessing data is FAST
* Don't worry about heap management like in OCaml and C++
* **Heap management** is slower than stack management

#### Disadvantages

* stack overflow :\(
* If you have a very successful program, then it will keep succeeding and building terms, and the stack might get too big.
* When the stack is enormous, they look in the stack for objects that cannot be referred to from here on out, and these objects are no longer accessible
* **Prolog interpreters are like heaps because this is a garbage collecting stack**
* Normally, the program is like a stack, but in practice, you still have the problems of a heap
* **If you try to write some random thing that succe**s**s all the time, then Prolog is probably NOT the best choice for efficiency**

## Debug

Use 'write', etc.

### Debugger model

```text
?- trace.
```

* **4 port model** 
  * think of a goal/subgoal, a debugger automatically put some print points when entering/executing the subgoal
  * if fail at a port, backtrack to the previous succeed port, continue, until goes to the fail port
  * One problem: lots of traversals, not recommended trying on large program
* For most programming languages, 2 port model \(just call function and return\)
  * e.x. c++, ocaml
  * Because they do not have backtracks

## Memory Management

* Prolog has a stack internally, if succeed, grow the stack; if fail, backtrack, thus shrink the stack.
* If a program keeps succeed \(a lot of successes\), the stack keeps growing, finally you will run out of stack space. So most prolog system has a **garbage collector** to collect the stacks that will not to referred anymore for future calculation.

## Unification

* a fancy word for "matching"
* e.x. 

  ```text
  member (X, [X|_]).
  ?- member(Y|L)
  (* unification *)
  (*{Y=X, L=[y|_29]}*) /* set of variable binding
                   or a unifier */
  ```

* A interpreter walks through two terms, trying to match by substituting values or variables. Or we can say by binding variables to value.
* Every time the interpreter does the matching, it comes up with a new unifier
* Like "match" in Ocaml, but in Ocaml, pattern matching works in only one direction, which means it matches e to something 

  ```ocaml
  match e with
  | [] ->
  | h::d
  ```

* But in Prolog, it can does **two directional matching**, i.e. you don't have to know what e is in order to do the unification \(matching\)

  ```text
  ?- m(E)
      m([]):- ...
      m([H|T]):- ...
  ```

  * Both directions can work simultaneously
    * p\(f\(X\),Y\) ?- p\(A,g\(B\)\)
      * it binds A with f\(x1\), and simultaneously binds Y1 with g\(B\)
      * A = f\(\_96\)
      * whenever it goes into unification, it creates local variables 
    * q\(f\(X\),x\) ?- q\(A,g\(B\)\)
      * it binds A with f\(X2\). and X2 with g\(B\), then A = f\(g\(B\)\)

### Trouble with two-directional unification

#### cyclic/infinite term \(\*not logical\*\)

```text
e(X,X) (*it successes only when two arguments are
        the same*)
?- e(f(x),g(x))
no, because two functions not possibly have same 
value

?- e(z,f(z))
{X1 = z, z = f(z)}
true. z = f(f(f(f(f... (*creates a loop somehow*)
(*This is called a cyclic/infinite term*)



```

* example: Peano arithmetic \(for natural numbers +\*-/ /for\_all /there\_exists logic
  * zero 0
  * succ\(E\) : successor of E 

```text
?- add(succ(succ(zero)), succ(succ(zero)), R) 

add(zero,N,N).
add(succ(N),M,succ(MplusN)):-add(M,N,MplusN).
sub(A,B,BminusA):-add(A,BminusA,B).
lt(N,succ(N)).
lt(M,succ(N)):-unify_with_occurs_check(M,N).
lt(M,succ(N)):-lt(M,N).

?- lt(H,H). 
H = succ(succ(succ(...
(*because it binds H with both M and succ(N)*)
```

* One solution: "unify\_with\_occurs\_check"
  * but this is slow, so people usually do not use it
* One more practical solution: avoid infinite terms in your program

## Pruning possible solutions

**cut !**

* efficiency, controls your computation, makes it faster without changing the logic

```text
generator(x,y,z), member(x,z), tester(x,y,z)
                |
                x = a
                z = {a,b,r,a,c,a,d,a,b,r,a}
member fun would run five times if keeps geting 
rejected
logically right but not good

=====solution======
membercut(x,[x|_]).
membercut(x,[_|L]):-membercut(x,L).
=====equivalently=====
membercheck(x,L):-once(member(x,L)).
```

```text
once(P) :- P,!.
(*if P succeeds, does a cut*)
```

A negation operator:

```text
\+(P) :- P,!,fail.  (*if P succeeds, cut, return 
                      fail; if P not succeed, 
                      backtrack*)
\+(_).

(* A   &   B     = true*)
?- x=3, \+(x=4).
x=3
(* B  = false*)
?- \+(x=4).
(*first proves x=4, then cut fail*)
no
```

### Closed World Assumption \(CWA\)

* if I don't tell you something about the predicate, it is false
* Suppose "everything that I don't tell you is false."

Dybrig $1-3,4

