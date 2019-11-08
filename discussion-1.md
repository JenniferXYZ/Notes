---
description: 10/04/2019
---

# Discussion 1

```ocaml
let x = 5;;
(*Ocaml knows x is an int because 5 is an int*)
(+);;
let plus x y = x+y;;
let plus_5 = plus 5;;
(*val plus_5: int -> int = <fun>*)
plus_5 6;;
(*int = 11*)
```

{% hint style="info" %}
int -&gt; int -&gt; int

int-&gt;\(int-&gt;int\)
{% endhint %}

```ocaml
let rec insert_n_lst n (x:int) lst = (*we specify x to be an int*)
if n = 0 then lst else x::(insert_n_lst (n-1) x lst);;
 (*int -> int -> int list -> int list*)
 
 
insert_n_lst 3 4 [6:7];;
(*int list = [4;4;4;6;7]*)  
```

If we do not specify x to be int:

```ocaml
let rec insert_n_lst n x lst = 
if n = 0 then lst else x::(insert_n_lst (n-1) x lst);;
(*int -> 'a -> 'a list -> 'a list = <fun> *)

```

{% hint style="info" %}
Here 'a means some type, as long as the elements in the list are of the same type, the function works
{% endhint %}

### List of mixed types:

```ocaml
type optional = Some of int | None;;
[Some 1; None; Some];;

type 'a optional = Some of 'a | None;; (*general type*)
[Some 1; None; Some 2];;
[Some 1; None; Some 2.];;

```

```ocaml
type ('nonterminal, 'terminal) symbol =
  | N of 'nonterminal
  | T of 'terminal
  
N 1;;
(* (int 'a) symbol = N 1 *)
```

\('a, 'b\) symbol = \('a N, 'b T\)

### Match

```ocaml
let plus_1 x = match x with
| Some y -> y+1
| None -> None;;
(*Error y is not Some type, but int*)

let plus_1 x = match x with
| Some y -> Some (y+1)
| None -> None;;
(*it works*)
plus_5 (Some 5);; (*returns 10*)
plus_1 None;; (*returns None*)

```

Exersice:

```ocaml
let rec insert_n n x lst = 
match x with
| _ when n = 0 -> lst
| None -> lst
| Some y -> y::(insert_n (n-1) x lst);;
(*int -> 'a optional -> 'a list -> 'a list*)

insert_n 2 (Some 1);;
(*return type: int list*)
insert_n 2 None;;
(*return type: 'a list, a weak type*)

```

{% hint style="info" %}
Weak type
{% endhint %}

```ocaml
let f g = g (g None)
(*val f: ('a option -> 'a optional) -> 'a optional = <fun>*)
(*
f: 'a -> 'b
g None => g: 'c optional -> 'd
g (g None): 'd -> 'b
'a = 'c optional -> 'c optional
'b = 'd= 'c optional
f: 'c (optional -> 'c optional) -> 'c optional
*)

```

```ocaml
let f g = g g;;
(* Error*)
(*
f: 'a -> 'b
assume g: 'c -> 'd
g g => g is 'c
       g is 'c -> 'd
       'c = ('c -> 'd)
       'c cannot equal to 'c->'d
*)

```

```ocaml
let get_some x = Some x;;

let p = (get_some 1, get_some 1.5);;
(*val p: int optional * float optional = (Some 1, Some 1.5)*)

let p some = (some 1, some 1.5);; (*Error*)
(*
p: 'a -> 'b
some 1 => 'a = int -> 'c
some 1.5 => 'a = float -> 'd
int != float
*)
```

### Define a recursive type

```ocaml
type 'a option = Some of 'a | None;;
type 'a bst = Node of ('a * 'a bst optional * 'a bst optional);;
(*Node of 'a contains a subtree of 'a optional type*)

```

{% hint style="info" %}
For a tuple of type, we use \* instead of value

\(int\*int\) = \(1,2\)
{% endhint %}

```ocaml
let tree = Node(let leaf_1 = Node (1, None, None);;
let leaf x = Node(x, None, None)::
let node_2 = Node(2, Some (leaf 1), Some (leaf 4));;
let node_5 = Node(5, leaf None, Some (leaf 6));;
let tree = Node(3, Some node_2, Some_5);;

```

Write a function for infix\_traversal: \[1;2;4;3;5;6\]

```ocaml
let infix_traversal tree lst = 

```

