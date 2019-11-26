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
* 
