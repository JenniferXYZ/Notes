---
description: 10/02/2019
---

# Lecture 2

Big backend queries at Google

Jane St. Capital



| language categories | example | unit | combination | characteristics |
| :--- | :--- | :--- | :--- | :--- |
| imperative | C/C++/Java/Python | command | S1;S2 sequencing |  |
| functional | Lisp/ML/Haskell | expression | function calls | less constraints, more opportunities for running in parallel |
| logic | Prolog | assertion | & \| -&gt; | no assignment statement, no function calls |

## Functional Languages

\(Function and function as argument\)

### Motivation 

Fortran \(numeric computation and scientific computing with arrays\) by J.Backus

* Clarity
  * Fortran code hard to read and follow \(e.g. i = i+1\)
  * Think about notations of derivatives in math \(v.s. dot notation\)

$$
d(x^2)/dx
$$

* Parallelizability 
  * No sequences, just function calls to make it easier to parallel

### More on functions

* Function: mapping from a domain to a range
* Functional form \(higher order function\): functions also live in domain
  * e.g. qsort in C
* Evaluation: Given an expression, what single value the function stands for. Order is given by pattern of calls. 

### Properties

No assignment statements and no side effects in functional programming

* no sequencing \(no ;\)
  * do f \( g\(x\) , h\( i\(y\) \), z \) \)
* no assignments \(no =\)
  * want your have referential transparency; thus easier to read code
  * helps clarity
  * helps performance \(can cache value in register, and match it with memory\) 
    * caching is easier in functional languages than convention languages
    * One example of horrible code \(not allowing things to change helps clarity\)

```
int h(int&a, int&b){
    a = 3;
    b = 4;
    return a; /*movl $3, %eax*/
}
/* call h(x,x), a and b same address*/
```



## Syntax

### Definition

* Syntax: how programs look: their form and structure
* form independent of meaning "semantics"
* Semantics: what programs do: their behavior and meaning

### Why now?

* it's easier
* it made us respectable

### Some English Examples

"Colorless green ideas sleep furiously." -N. Chamsky

* syntactically correct but semantically nonsense

"Ireland has leprechauns galore." -P. Eggert

* syntax horrible but semantically right

"Time flies."

* N. V or V. N
* A common problem in natural language \(and also computer language\): ambiguity 

> Ambiguity--normally a bad thing in programming language.
>
> E.x. a = b + c + d \(different parentheses give different results due to rounding\)

### Syntax Choices

\(Reason to pick one syntax over another\)

* Inertia
  * Pick a syntax that is familiar to people
* Simple and regular \(competing objectives with Inertia\)
  * People prefer short and simpler grammar, thus easier to explain
* Readability \(visually\)

```
match E with
| [] -> empty_set
| h_ -> h
```

* Writablity
  * e.x. APL \(a programming language\) 
* Redundancy
  * it makes you repeat yourself a little bit
  * helps you catch error \(think about parenthesis match in C\)
* Unambiguous 

### Tokens

\(i.e. categories of lexemes\)

* building blocks of syntax
* character set 
  * ASCII -- 7 bit set in 8-bit byte
  * Unicode -- 29\(?\)-bit set \(under scheme of UTF-8\)

```
{ 
int o = 19; /*Ascii*/
return o; /*Cyn*/}
/*returns 47 instead of 19*/
```

```
IJK=27
I J K =27
DO 10 I=1,100
    (body of loop)
    10 CONTINUE
```

Someone made a typo: 

```
DO 10 I=1.100
DO 10I = 1.1
```

{% hint style="info" %}
White space matters 
{% endhint %}

* keywords and reserved words
  * i \(identifier\)
  * iff \(identifier\)
  * if \(IF\)
  * Some languages without reserved words
    * PL/I
  * **Keywords**​ have a special meaning in a language, and are part of the syntax.
  * **Reserved words**​ are words that cannot be used as identifiers \(variables, functions, etc.\), because they are reserved by the language.
    * Reserved words violate the mutability principle since it’s not possible to add new keywords since that would break a lot of previous code.

## Grammar

### Parse Tree and Grammar

* We use a parse tree to represent a grammar
* Grammar for programming languages defines an infinite language; expressions can be arbitrarily long, recursive.
* As long as the grammar generates at least one parse tree for a given string of tokens, that string is in the language. 
* Grammar specifies what type of parse trees you can create from a set of tokens

### Context free grammar

* the set of **tokens**
* the set of **non-terminal symbols**
  * strings enclosed in angle brackets, such as &lt;NP&gt;
  * e.x. statements and expressions
* the set of **productions** 
  * consists of a left-hand side \(a single non-terminal symbol\), the separator ::=, and a right-hand side \(a sequence of one or more things\)
  * it permits right-hand side to be children in the parse tree
* **start symbol**: a particular non-terminal symbol
* **terminal rules**: tokens or the leaves
* If you want to prove that your line of code is correct, then it has to be separated into tokens and you have to create a valid parse tree according to the grammar that you’re given. And that grammar contains the rules that allow you to create the tree.
* A grammar is **ambiguous** because you could have multiple different parses because of the addition and multiplication, so we need to figure out another rule so that we can avoid getting two different trees.

