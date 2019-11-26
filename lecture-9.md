---
description: 10/28/2019
---

# Lecture 9

## Logic Programming

### Comparison of programming languages

|  | Imperative Programming | Functional Programming | Logic Programming |
| :--- | :--- | :--- | :--- |
| Example | C++, Java | Ocaml | Prolog, Lisp |
| Loops | Yes | **NO** | **NO** |
| Assignment Statements | Yes | **NO** | **NO** |
| Recursions | Yes | Yes | Yes \(queries\) |
| Functions & Calls | Yes | Yes | **NO** |
| Predicates and Assertions | Yes | Yes | **NO** |

### Algorithm = Logic + Control

* True for C++, Java and functional languages
* A for loop is sorta an algorithm
* In conventional programming, you combine logic and control together into one program; **with logic programming, one of the goals is to specify** _**what control to use**_**.**
* **Control** should not affect what answers you get since you get the same T/F answers whether true or false. It is concerned with how **efficient** the implementation is. 

### Example of splitting big problem to sub-problems

Sorting: 

* E.x. Quicksort, Heapsort, Bubblesort, Insertionsort etc.
* IDEAS:
  * **No functions in Prolog, so write predicates**
  * **Initial caps for variables, initial lowercase for predicates!**
  * **Feed its output as S and input as L**
  * **:- for if**
  * S has to be a permutation of L
  * All elements in S have to be in non-decreasing order
  * For all L and all S, if perm and sorted is true, then sort is true!
* Base cases for recursion come first
  * understand east stuff first
* Naming are important when writing programs
  * Non-decreasing is better than ltfe
* **When stuck, it is recommended to draw pictures of what is going on**

  ```text
  ------------------------
  sort(L,S) :- perm(L,S), sorted(S)
       | |              |
       | |              |
       | |              +> and
       | +> sorted
       |  "equivalent"
       |
    any list
   of integers
  -------------------------
  Permutation(L,S)
  +---+---------+
  | H |    L    |
  +---+---------+
           |
           |     perm          +--------+---+----+
           +-------------> S = |   R1   | H | R2 |
                               +--------+---+----+
  ```

  * If there is no H in S, then is not a permutation of L
  * Permutation is defines recursively in terms of itself, and that is the key way this code is going to work

## Prolog

* **Atoms** are indivisible - equal to only themselves
  * Individual units of computation that you cannot divide up and look inside them
  * insist on being individualists
  * Numbers are like atoms
* **Variables** \(logical variables\)
  * Have an initial capital letter or underscore
  * As you keep computing successfully, the variable never changes
  * It might fail
  * When you made the wrong decision, you have to backtrack 

### Prolog program structure

* Terms don't have to be simple, it can be complicated
* \_ is a don't-care variable analogous to Ocaml

### Rules

* conditional expression of the form: **consequence :- antecedence**
  * consequence is a single term
  * antecedence is one or more terms separated by commas

### Queries



