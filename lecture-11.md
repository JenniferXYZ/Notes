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
* 


