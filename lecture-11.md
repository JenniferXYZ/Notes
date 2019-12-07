---
description: 11/13/2019
---

# Lecture 11

## Syntactic Sugar

```text
[]       =  '[]'
[x|L]    =  '.'(x,L)
[x,y|L]  =  '.'(x,'.'(y,L))
[x,y,z]  =  '.'(x,'.'(y,'.'(z,[]))))
```

## Definite Clause Grammars

* Prolog built-in feature: Syntactic Sugar
* Instead of +, \*, =, this lets you write parsers more efficiently or easily than you would in Prolog
* Put terminal symbols in square brackets \[\]

## Prolog Theory

* Based on mathematical logic

### Propositional logic

* "It is raining." = P
* "Traffic is busy on the 405." = Q
* Some people may say it is true or false. But we can assume it is either/or
* We give each of the propositions arbitrary names, and assume each is either true or false
* We can also have connectives which let us build larger propositions out of smaller ones
  * P ^ Q , P V Q , P -&gt; Q
* Prolog equivalent of AND, OR, and IMPLIES
  * P ^ Q =&gt; P , Q 
    * AND is commutative and associative
  * P V Q =&gt; P ; Q
    * OR is commutative and associative
  * P -&gt; Q =&gt; P :- Q
    * IMPLIES is NOT commutative and associative
    * equivalent to ~P V Q
* Tautology: a statement in propositional logic that is true regardless of what the values are for the elements that compose the statement
  * these tautology are redundant since they're independent of what the constituent values are

### First Order Logic \(FOL\)

Also called predicate calculus

#### Example

\(1\) All men are mortal. \(2\) Socrates is a man. \(3\) Socrates is a mortal.

FOL says the first two has to imply the 3rd. We cannot however prove this with propositional logic since there isn’t a set of connectives we can use to represent this new statement.

* In FOL, propositions can have arguments
  * “Freeway X is busy” = P\(X\) and “It was cold on day Y” = Q\(Y\)
* We can also have "for all" as well as "there exists"
* An example of a tautology in FOL 
  * For all X, \(P\(X\) -&gt; Q\(X\)\) ^ P\(a\) -&gt; Q\(a\) 
  * For all X, \(P\(X\)\) &lt;-&gt; ~There exists Y ~P\(Y\)

### Clausal form

* Clausal form is a simplified version of predicate calculus/FOL. Can take any set of predicate calculus statements and turn them into a set of equivalent clauses
* Horn clause simplified assumptions by saying that n &lt;= 1.3 possibilities
  * Horn clause:  A Horn clause is a [clause](https://en.wikipedia.org/wiki/Clause_%28logic%29) \(a [disjunction](https://en.wikipedia.org/wiki/Disjunction) of [literals](https://en.wikipedia.org/wiki/Literal_%28mathematical_logic%29)\) with at most one positive, i.e. [unnegated](https://en.wikipedia.org/wiki/Negation), literal.
    * If n=1, m=0, then you have a Prolog fact
      * e.x. man\(Socrates\)
    * If n=1, m&gt;0, then you have a Prolog rule
      * e.x. mortal\(X\) :- man\(X\)
    * if n=0, then you have a Prolog query
      * e.x. ?- mortal\(Socrates\)
* slow, complicated
* hard to think about

### Proof by contradiction

* Prolog goes by truth by contradiction. 
  * Assume some query is false, then you show ~m, p, q, r... is false, then the whole thing is true since you have found a contradiction

## Storage Management

*  RAM
*  Fit the program into RAM as much as possible

### What do we have to manage?

* static variables - stay alive as long as the program is alive
* static code - We know the exact location of the code!

### One solution 

* **Stack**
* Put local variables onto the stack
* auto - like static except local variable to the function
* This would save things in a “temp”
* Local variable that you didn’t declare but the compiler declared it for you
* f needs to know where to return to
* On x86-84, it is stored in memory
* Manage return addressees
*  Program will have to manage the memory that contains the data and the code
*  Have a manager of some sort to help us do this
* Standard library will be the C library and called **memory manager**

### Memory Manager

* the machine code that manages the memory
* library manager that manages all these
* if memory manager cannot get enough memory, the whole system falls apart
* **Gives itself priority**
* **Multithreaded too**

## Array Layout

* Key: find the address of the head of the array
* ideally, accessing array should be as fast as possible
* Multiplying two n-bit algorithms are O\(n^2\)
  * It can be faster when we use shift operator
* Get rid of substract
  * have the pointer point at the 0th entry of the array even if it does not exist

