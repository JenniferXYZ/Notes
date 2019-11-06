---
description: 09/27/2019 Ocaml basics
---

# Discussion 0

Seasnet server: lnxsrv 06,07,09,10

## Built-in Types

### int and float

{% hint style="info" %}
Float cannot be added. To add float, we need a dot after + \(e.g. 1+.2.;;\)
{% endhint %}

```
23;;
```

Output: int = 23

```
23.;;
```

Output: float = 23

```
1.+2.;;
```

Output: Error, float cannot be added

```
1. + .2.;;
```

Output: float = 3.

### Boolean

```
let bool = true;;
```

Output: val bol: bool = true

```
not bool;;
```

Output: bool = false

### String

```
"hello world";;
```

Output: string = "hello world"

### Void

```
let uintvar = ();;
```

Output: var uintvar: unit = \(\)

## Variables

{% hint style="info" %}
Use keyword "let"
{% endhint %}

```
let x = 5;;
let x = "string";;
```

## Function

```
let add_int x y = x + y;;
```

val add\_int: int-&gt;int-&gt;int = &lt;fun&gt;

```
add_int 1 2;;
```

Output: int = 3

```
let add_float x y = x +. y;;
```

val add\_float: float-&gt;float-&gt;float=&lt;fun&gt;

```
let x = 5 in x+1;;
```

```
let five = let x =2
in add_int x 3;;
```

Output: val five:int=5

```
let five =
let x = 2 in 
let y = 3 in
let ret = add_int x y in
ret;;
```

Output: int = 5

```
let anti_div x y = 
let y = x
and x = y in
x / y;;
val anti_div 2 10;;
```

Output: int = 5

## Environment/Expression

{% hint style="info" %}
Everything inside an expression is local.
{% endhint %}

```
let ten = 
    let x = 2 in
    let y = 
        let x = 3 in
        x + 4 in
    1 + x + y;;
```

Output: val ten: int = 10

## Recursion

{% hint style="info" %}
Keyword **rec** before the function
{% endhint %}

```
let rec factor x = if x <> 0 then x * factor (x-1) else 1;;
factor 3;;
```

Output is 6

{% hint style="info" %}
For each **if** expression, we **must** have an **else**
{% endhint %}

```
if 3 > 2 then 3 else 2;;

if 3 > 2 then 2;;
(*Error: expect an else expression*)
```

## List

* all elements in a list must be of same type
* Some predefined functions
  * :: push an element into the list
  * @ concat: need to make sure type consistency
  * length
  * map
  * filter
  * fold\_left

```
let lst = [1; 2; 3];;
0::lst;;
(*int list = [0; 1; 2; 3]*)

[1; 2]@[3; 4];;

List.hd [1; 2; 3];;
(*int = 1*)
```

{% hint style="info" %}
Use predefined function when available \(here are some on course page\)
{% endhint %}

```
let lst = [1; 2; 3] in 
let double x = 2 * x in 
List.map double lst;;
(*int list = [2; 4; 6]*)

let lst = [1; 2; 3];;
List.map (fun x -> 2 * x) lst;;
(*int list = [2; 4; 6]*)

List.filter (fun x -> x mod 2 = 1) lst;;
(*int list = [1; 3]*)

let add_int x y = x + y;;
List.fold_left add_int 0 lst;;
(*int = 6*)
```

\*\*\*\*

**Exercise:** define a function odd\_sum\_to : int -&gt; int which gives the sum of all odd numbers that is equal to or smaller than the value we pass. Example: odd\_sum\_to 10 = 1+3+5+7+9=25

\(I forgot the base case\)

```
let rec odd_sum_to x = 
    if x = 0 then 0 (* comment: base case hehe*)
    else if x mod 2 = 1 
        then x + odd_sum_to(x-2)
        else odd_sum_to(x-1);;

```

```
let rec up_to x = 
    if x = 0 then []
    else x::up_to(x-1)
List.filter (fun x -> x mod 2 = 1) list
List.fold_left add_int 0 list
```

Sometimes you need a parenthesis 

```
double add_int 1 2;;
    error
double (add_int 1 2);;
int = 6
```

## Tuple

```
(1, 2.);;
(*int * float = (1, 2.)*)

let f x = (x, x+1, x*2);;
f 3;;
(*int * int * int = (3, 4, 6)*)
```

## Match Statement

```
match (3,4,6) with 
| (3,x,y) -> x+y
| _ -> 0;; (*underscore means we dont care about the value*)
int = 10

match (3,4,6) with
| (_, 4, z) -> z  (*first line has priority*)
| (3,x,y) -> x+y
| _ -> 0;;
int = 6
```

{% hint style="info" %}
match statements should be exhaustive, must use -&gt; not =
{% endhint %}

```
match (12,0,12) with
| (_, 4, z) -> z;;
(*Error: not exhaustive*)

match (2,3,4) with
| (_, 4, z) -> z
| (x, _, _) -> x;; (*exhaustive*)
(* int = 2 *)
```

## Type

```
type week = Sun | Mon | Tue | Wed | Thu | Fri |Sat;;
let week_to_num day = match day with
| Sun -> 0
| Mon -> 1
| Tue -> 2
| Wed -> 3
| Thu -> 4
| Fri -> 5
| Sat -> 6;;
week_to_num Mon;;
(* int = 1 *)

type number = Int of int | Float of float (*Enumerator*)
Int 4;;
(* number = Int 4 *)
Float 2.;;
(* number = Float 2. *)
[Int 1; Float 2.];;
(* number lists = [Int 1; Float 2.] *)

```

{% hint style="info" %}
Use **match** together with **Enumerator**
{% endhint %}

```
let rec float_sum lst = match lst with
| [] -> 0.
| （Float x）::rst -> x +. float_sum rst
| (Int x)::rst -> (float x) +. float_sum rst;;
```

## Grammar

\(Remember to copy the following lines to hw1\)

```
type ('nonterminal, 'terminal) symbol =
  | N of 'nonterminal
  | T of 'terminal
```

The following is an example of grammar:

```
starting symbol <Expr>
rules: 
    <Expr> ::= <Num><Op><Num>
    <Num> ::= 1|2
    <Op> ::= +|-
```

