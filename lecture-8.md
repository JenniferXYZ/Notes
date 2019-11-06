---
description: 10/23/2019
---

# Lecture 8

## Java Background

* workstations and servers all in Solaris \(on C\)
* early 1990's: IOT, uses embedded devices, mostly in SPARK or x86 
* If they want to run, needs compile twice in SPARK & x86
* PROBLEMs: 
  * hassle to unite portable code and multiple build
  * not Object-Orientated \(easy for programming tho\)
    * They want to solve it by using C++, but C++ is too complicated
  * Reliability problem: too many crashes; we want to report system to be convenient for all programs
  * the internet speed in low Rkb/s. If update, then that would be slow \(Bloated executables\)
* Steals ideas from Xerox PARC, they invented Smalltalk \(O-O\) language

  **Object oriented and simple**. It also compiled the source code into machine independent bytecodes, and then to make it work on different machines you need to create bytecode interpreters, which were not too difficult to create.

  * interpreted/portable language -&gt; byte code formal
    * garbage collection for memory
    * subscript checking etc.
    * IDE
  * Smalltalk
    * has bizarre syntax \(training issue\)
    * dynamically typed
    * fast networking

* Smalltalk + C + C++ =&gt; Oak \(a new language\)
* Then the lab turned to focus on browser
  * Mosaic \(UIUC, M. Andreeseen\), first successful browser
  * www
  * Mosaic was written in C++, crashed a lot
  * Some people tried using Oak =&gt; Java to write a Mosaic-like brower in Hot Java, which did not crash a lot and is more extensible \(HotJava is a browser written in Java\)
  * HotJava had applets, which are downloaded from the website to the browser \(via bytecodes over network\), and thus you could extend the functionality of your browser.
  * Mosaic had their own version in the form of plugins, but didn't work as well.
  * Applets had a problem in that it was a good match for servers but not really for clients, since there was a lot of work in parallelism and was over-engineered and heavyweight for the clients. 
    *  So you run Java on the server side but not on the client side.

## Java basics

### **Types in Java**

* **Primitive types**
  * primitive types are precisely specified 
  * Primitive: Byte \(like char in C\), char, short, int, long, float, double, boolean
  * There’s **no address of operator \(&x\)** in Java
  * In C++, you can have different machines that have different bit sizes for ints, longs \(32/64\), etc. But in Java, these values \(32 for int, 64 for long, etc\), these are hardwired down. All the machines have to abide by IEEE format. Java is very big on **portability**.
  * Overflow:
    * if Java integer overflows, wrap semantics: given the lower bits
    * if C int overflows, undefined behavior
  * Results of calculations maybe be different by different Java interpreters

    ```
    a * b + c
    ```
* **Reference Types \(**values that point to places in memory**\)**
  * all the objects: arrays, classes 
  * drawbacks: cannot be generic programmed

### **Arrays in Java \(reference type\)**

* always live in the heap. Only way, use "new" 
* always objects

```
Int [] foo = new int [100]; 
```

* Java has a garbage collector so this array will always stay there and thus they are always heap allocated. They also have a **fixed size once allocated**. You can also return arrays from methods. Subscript checking when trying to access an array is required. Arrays are also **initially zero** when you create them.

Example:

In C, y cannot be changed. If y is a pointer, you are not allowed to change the value of y.

```
int func(){
    struct s {int a[10];} x,y;
    x = y; /*copys 10 ints*/
}

int f(){
    int x[10];
    int y[10];
    y=x;
} // error
```

```
int f(){
    int x[10];
    int y[] = x;    
} y = z;
```

### **Inheritance** 

* Java has only single inheritance, classes inherits from only one parent. Thus the object hierarchy is a tree and the root of the tree is the class object.
* C++ has multiple. 

### **Interface**

* The substitute for multiple inheritance is called an Interface. 
* Defines what a class **must be able to do, not how to do**
* Interface **cannot be instantiated**, much create a class that implements that interface
* Parent has m\(\) and n\(\). The child gets those 2 methods and that saves work. With an interface, though, it’s like you’re inheriting a debt which means that if the child implements the interface \(Let’s say the inheritance declares o\(\) and p\(\)\), then the child has to implement o\(\) and p\(\). 
* The interface placed a constraint on the child’s behavior.

```
public class Rectangle{

}
public interface Drawable{
    void drawAt (location); // Not implementation
}

public class Drawable_Rectangle
    extends Rectangle
    implements Drawable{
        void drawAt (location x)
    }
{
    /*CODES*/
}    
```

* You are allowed to implement as many Object as possible
* **Why using interface:**
  * to achieve total abstraction.
  * java does not support multiple inheritance in case of class
  * to achieve loose coupling.
  * Interfaces are used to implement abstraction. Abstract classes may contain non-final variables, whereas variables in interface are final, public and static

### **Abstract class \(think it as API\)**

* A combination of a class and an interface
  * cannot create an object using an abstract class
  * can define some parts of the class, while leaving other implementations for children
* Classes can extend only one abstract or normal class
* An abstract class is where you have some methods implemented but some that are declared but not defined. 

  ```
  class p{
      int m(){/*code*/};
      int n(){/*code*/};
      abstract int foo();
  }
  ```

* Basically supply initial code to the subclasses, but there are some holes for the child classes to define themselves. 
  * This is kind of the combination between classes and an interface.

    * An abstract class is useful to be parent of other classes.

    ```
    New Rectangle(); //okay
    New Drawable(); // not okay, it is an interface, not an executable
    New AbstractList; // not okay, there are holes in it
    AbstractList x = New Linkedlist(); //okay
    ```

### Final class

* Final classes have no children
  * method cannot be overridden
  * runtime will be less if only use final class because final class cannot be overridden/overwritten
  * allows inline
  * dont trust the children, prohibits children misbehavior

### Things to do: 

Read Java standard Library

* abstract list
* LinkedList
* List
* Object \(what they do\)

