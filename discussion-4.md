---
description: 11/01/2019
---

# Discussion 4

## Declarative Language

You don't write down algorithm, you only write down the goal.

E.x. SQL

## Prolog

* two parts: file.pro / .pl + gprolog \(interpreter\)
* gprolog: 
  * queries 
* file.pro

  * fact 
  * rule

  ```text
  lower_case -> fact

  ?- [temp]

  // temp.pro
  color(sun, red)

  ?- color(sun, red).
  returns yes

  ?- color(sun, Color).
  returns Color = red

  ?- color(What, Color)
  returns Color = red What = sun
  ```

* lower\_case -&gt; fact
* upper\_case -&gt; variable

```text
is_type(bool).
is_type(int).
of_type(t, bool).
of_type(f, bool).
of_type(1, int).
of_type(2, int).
of_type(3, int).
of_type(1+2, int).

//Queries
?- is_type(Type)
Type = bool?
(*if accept, press enter*)
yes

Type = bool? ; (*put a ; if do not accept answer*)
Type = int
?- is_type(float).
no
?- of_type(one, Type).
Type = int

of_type(Value, Type). 
(*Prolog will interate thru all possible comb until
you accept the anser*)

of_type2(t, is_type(bool)). (*this is actually a tree*)
?- of_type2(Value, Type).
Value = t
Type = is_type(bool)

?- of_type(1+2,Type).
Type = int

?- of_type(1+1, Type).
no (*because we did not define 1+1, 1+1 and 2 forms
two different trees*)
    of_type            |        of_type
 +            Type     |       2        Type
1  1                   |
(*similar to Ocaml's match*)


```

### Unification

```text
(*unification*)
match (1, (2, "a")) with
    | x,y -> x=1 y=(2,"a")
    | x,y,z -> x

(* "=" is a built-in relationship, unification *)
?- 1+2 = +(A,B).
A = 1
B = 2

?- of_type(A,int) = of_type(2+3,Type).
A = 2+3 (*syntax sugar: +(2,3)*)(*this is a tree*)
Type = int

```

### Grammar in prolog: 

```text
term : = atom 
    | Relation
Relation := atom(term+)
```

### Rules

#### is

* evaluates rhs and compare it to lhs
* only evaluates rhs

```text
?- 2 is 1+1.
yes
(*evaluate rhs and compare it to lhs*)
?- X is 1+1.
X = 2
?- 1+1 is 2.
NO (* "is" only evaluates rhs*)

```

#### =:=

* makes comparison

```text
?- 1+1 =:= 0+2.
yes

?- x =:= 0+2.
error
```

#### =/=

* unequal

#### =&lt; ; &lt; ; &gt; ; &gt;=

#### :- 

* if

```text
of_type(Sum, int) :- 
    Sum = +(X,Y),
    of_type(X, int),
    of_type(Y, int).
    
?- of_type(+(3,3), Type).
Type = int

?- trace. 
?- of_type(+(3,3), Type).
(*this will trace how prolog implements the query*)
?- notrace. (*to stop trace*)

of_type(if(Cond, Then, Else), Type) :-
    of_type(Cond, bool),
    of_type(Then, Type),
    of_type(Else, Type).
(* if X then Y else X => returns a T type*)

?- of_type(if(1,2,3), Type).
yes
?- of_type(if(1,1,3), Type).
no (*becuase 1 is already a bool type*)
?- of_type(if(t,1,1+2), Type).

?- of_type(if(t,A,f),int).
error, stack overflow (*if returns bool, not int*)


```

### List

```ocaml
[1;2;3];; 
1::2::[3];;
H::T (*head to tail*)
```

```text
[1,2,3].
[1,2|[3]].
[H|T]. (*head to tail*)

```

#### is\_member

```text
(*if x is an element of list*)
is_member(x,[x|_]).
is_member(x,[_|t]) :- is_member(x,t).

?- is_member(2,[1,2,3,4]).
true ?
yes

?- is_member(x,[1,2,3,4]).
x = 1? (*iteratively, it tries to figure out wht x is*)

?- is_member(5, [1,2,3,x]).
x = 5?

```

#### append

```text
app([],Lst,Lst).
app([H|T], Lst, [H|Tmp]) :- app(T, Lst, Tmp).
                    |
 (*we cannot put app function here directly, 
 because it does not return a relation*)
```

#### quicksort \(recursive function\)

```text
qsort(input, output)
    input: [Pivot|Tail]
    Output: [app(less,[Pivot|Great])]
        qsort(p1,less)
        qsort(p2,great)
        split(Tail, Pivot, p1, p2)
```

```text
qsort([],[]).
qsort([H|T], Output) :- 
    split(T,H,Less,Great),
    qsort(Less, LessSorted),
    qsort(Great, GreatSorted),
    app(LessSorted,[H|GreatSorted], Output).
    
split([],_,[],[]).
split([H|T],P, [H|L2],G2) :-
    H <= P,
    split(T,P,L2,G2).
split([H|T],P,L2,[H|G2]) :-
    H > P,
    split(T,P,L2,G2).    
    
```

### Example: Magic Square

Magic square:

1. \(nxn\) matrix of \(1,2,...,nxn\)
2. sum of each row = same
3. sum of each col = same
4. sum of dig = same

   ```text
   e.g.
   4 9 2
   3 5 7
   8 1 6
   ```

   ```text
   contain_less(_,0).

   contain_less(List,X) :-
     member(X, List),
     X1 is X-1,
     contain_less(List, X1).

   permut(Lst, N) :-
     length(Lst,N),
     contain_less(Lst,N).

   msq3([[A11, A12, A13],
         [A21, A22, A23],
         [A31, A32, A33]]) :-
     permut([A11, A12, A13, A21, A22, A23, 
           A31, A32, A33], 9),
     Sum is A11 + A12 + A13, (*after permut, numbers
                               are known*)
     Sum is A11 + A12 + A13,
     Sum is A21 + A22 + A23,
     Sum is A31 + A32 + A33,
     Sum is A11 + A21 + A31,
     Sum is A21 + A22 + A32,
     Sum is A31 + A32 + A33,
     Sum is A11 + A22 + A33,
     Sum is A31 + A22 + A13.                          

   (*This solution is slow*)
   (*You can use better strategy by using diff
     orders of operations*)

   ```

* an acceleration

  ```text
  contain_less(_,0).

  contain_less(List,X) :-
    member(X, List),
    X1 is X-1,
    contain_less(List, X1).

  permut(Lst, N) :-
    length(Lst,N),
    contain_less(Lst,N).

  msq3([[A11, A12, A13],
        [A21, A22, A23],
        [A31, A32, A33]]) :-
    fd_domain([A11, A12, A13, A21, A22, A23, 
          A31, A32, A33], 1, 9),
    fd_all_diffrent([A11, A12, A13, A21, A22, A23, 
          A31, A32, A33]),
    Sum #= A11 + A12 + A13, (*after permut, numbers
                              are known*)
    Sum #= A11 + A12 + A13,
    Sum #= A21 + A22 + A23,
    Sum #= A31 + A32 + A33,
    Sum #= A11 + A21 + A31,
    Sum #= A21 + A22 + A32,
    Sum #= A31 + A32 + A33,
    Sum #= A11 + A22 + A33,
    Sum #= A31 + A22 + A13.                          
    fd_labeling([A11, A12, A13, A21, A22, A23, 
          A31, A32, A33]).
  (*this method draws the solution at its last
  step, so it is much faster*)

  ```

### Example: Sequence

Generate a decreasing sequence starting with n

E.x. seq\(Lst,3\) -&gt; \[3,2,1\]

```text
seq([],0) !. (* "!" checkpoint*)
(*so when N<0, it will stop*)
seq([N|T], N) :- (*becuase N will be the head of ret*)
    N1 is N-1,
    seq(T, N1),
    !.
```

{% hint style="info" %}
! checkpoint: Prolog backtracks from checkpoint to end

Sometimes it would accelerate program, but only use it when you are sure about the result of "cutting unnecessary branch".
{% endhint %}

{% hint style="info" %}
Tips:





f\(x-1, ...\) 

X=X-1 does not work, use IS

=&gt; f\(x-1,...\)

X1 is X-1
{% endhint %}

### Tips

* Grammar -&gt; book
* Library: Function/ Relation -&gt; Kimmo's slides
* f\(x-1,...\)    x=x-1 does not work
  * x1 is x-1, f\(x-1, ....\) is correct
* uncons exception: instantiation 
  * x is y \(member\(y,\[1,2,3\]\)
  * x =:= y unknown
* infinite loop \(very slow, stack overflow\)
  * order works
* accelerate 
  * cut ! \(be attention to the side-effects\)

