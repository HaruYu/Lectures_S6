---
title: Compilation CCMP1
author: trinh_v
...

# Compilation course_2018-01-29
[Lectures Slides](https://www.lrde.epita.fr/~tiger/lecture-notes/slides/ccmp/ast.pdf)

## TYLA Language Typology (fin avril)

* History computing
* History of programming
* The handling of routines in various languages
* History of OO languages: Simula, Smalltalk, C++
* The Eiffel programming languages
* Let's go!

## CCMP Compiler construction

* Development tools
* A flex scanner with locations and symbols
* AST
* Names, scop, bindings
* type checking
* intermediate representation
* instruction selection
* instruction scheduling
* liveness analysis
* register allocation
* garbage collection

***

$a+b$ est-il valide?
 \_\_-> Liaison de nom (savoir où sont définies les variables)  

Généralement, 32 registres. S'il y a 33 variables? Utilisons la pile.

***

## Introduction to Tiger Compiler

The needs

* EPITA asked for a long and challenging project
* Should be a *potpourri* of every subject from computer science courses tought in third year

This gives a compiler construction project

It's a complete project

*  Specification
* Implementation
* Documentation
* Testing

Several iterations

* 5 steps
* 3 months

Chose our own strategy. team management

Project in `C++`:

* High and low level constructs
* Oriented Object design and Design pattern

Development tools:

* Autotools, Doxygen, Flex, Bison, GDB, Valgrind, Git.

Understanding computers

* Compiler and languages are tightly related to computer architecture

English

* Obviously

### Overview

Tiger is a language designed by Andrew Appel (he wrote 3 books: C language, Java language and ML). The Java is bad because the writer was bad
\_\_-> We chose the ML bool. Modern compiler implementation in ML

The compiler can be non-deterministic

* For example using inline or optimizing

The project will need some modules to do other ones **We'll have to do everything**. The code has gaps.
We'll have to write ~5000 lines of code
Documentation of 250 pages.

* homepage of the project: [www.lrde.epita.fr/~tiger](www.lrde.epita.fr/~tiger)
* news.epita.fr: `cours.ccmp`

#### Rules

* No copy between groups
* Fixing mistakes earlier is better (should keep a file)

#### Evaluation

Defenses and moulinette

## GCC steps

1. `cpp` preprocessor (lexical, expand macros) (syntax, work on syntax)
2. `cc1` Compilation (traduction from source to dest)
3. `as` (assembler)
4. `link` (linker)
-> a pipe

![img](totor.png)

Narrow compiling (line by line) losing contexts != large compiling which is taking the whole file and parse it

 ***

## Tiger Development tools

* One module, one namespace.
* One library per module with pure interface (libfoo.\*)
* One task set per module, maybe impure (task.\*)
* Task describe the command line interface
* Requirement over tasks order
* 3 file types .hh .cc .hxx

### Autotools

See Alexandre Duret-Lutz's tutorial. [Duret-Lutz, 2006]

#### Packages

* Autoconf
* Automake
* libtool
* gettext
* flex

`-pipe` utiliser les redirections dans Autotools

### Other developing tools

* Use warnings
* use assert macrosuse static_assert
* clang tidy, clang format
* DUMA, PageHeap(Windows)
* Dmalloc
* AddressSanitizer, ThreadSanitiwer, memorySanitier, Leaks Sanitizer
* Icov
* Mudflap
* GDB
* Purivy, insure++
* Valgrind
* intel pin
* DTrace
* Clang Static Analyzer

***

## Abstract Syntax Trees

Why do we need an AST? Because we can go through easily
Construct the smallest AST possible. Get through every useless things.

### Building an AST

Bottom building using `Flex` and `Bison`

Other possibility : SDF --Syntax definition formalism-- **BUT** very slow.

Build the AST by hand using `Bison` and `flex`.

#### Problems to avoid

```bison
_____ { return new myvar(); }
instead use
_____ { return make_var(); }
```

How to stock the AST? `Json` or `XML` serialization

* Protobuff
  * Serializes and deserialize an AST

```C++
class Bin: public Exp
{
  public:
    Bin(char oper, Expr* lhs, Exp* rhs)
      : Exp(), oper_(oper), lhs_(lhs), rhs_(rhs)
    {}
    ~Bin() override
    { delete lhs_; delete rhs_; }

  private:
    /* FIXME */
}
```

Types in compiler:

* pretty printer (const)
* name analysis
* unique identifiers "which 'a' are we talking about?"
* Desugaring while > goto
* type checking (can be const or not)
* non local (escaping) variables
* inlining

##### Problems

Overloading operator<< doesn't work because it's not in the class
Instead, use a method in the class ``b.print();`` >> There's no module.
\_\_;-> Create module and create a function `print(exp)` outside the class.

###### _Multimethods_

```C++
using std::ostream;
ostream& operator<<(ostream& o, virtual const Expr& e);
ostream& operator<<(ostream& o, virtual const Bin& e);
ostream& operator<<(ostream& o, virtual const Num& e);
```

this doesn't works.

###### Visitors

```C++
#include <iostream>
// Fwd.
class Exp;
class Bin;
class Num;

class Visitor
{
  public:
    virtual void visitBin(const Bin& exp) = 0;
    virtual void visitNum(const Num& exp) = 0;
};
```
***

# Compilation course_2018-01-29

Define data structures: classes hierarchy.
Bad idea using template and virtual. This won't work.

We can instantiate an evaluator for each recursions

`` xalloc `` can add parameters to ``<<`` operator

tiger syntax: ``if then ... else ... `` is void type

```
a | b
    if a then 1 else b <> 0
a & b
  if a then b<>0 else 0

a < B < g

```

Handle the side effects for example when a & b & c

***

## The scanner and the parser

Symbols : we can determine the language

### Bison and Flex

## Scope and variables

Scope: Area where a variable is defined and where it is accessible.

A symbol is associated to a memory area. If the symbol dies, the memory area isn't necessary freed

Diferents scopes:

* {}
* If ending at the end of else
* enums
*

```C++
  int N = 42;
  void foo (int i, int j = N);
```

We need scopes to do modularity work.

### Binding

### Symbol table

Every nodes of the AST has a parent field, which allows to get previous definitions >> NOPE.
Use an hash map that is copied in a stack
Environment and type checking

#### Hashtable

A scope is an hashmap, and push it on a stack

---

# 19-02-2018

***

Link break to while
continue to loops
If to else (it is already linked in the AST node )
return to functions

Link functions, types
Handle overloading
Find the variable that is masked, not the ones that are alive in a scope

---
# 05-03-2018: Types
***

Why'd we use types?
Instructions in assembly language are typed. However, the data is not typed.

Using types is useless and complicated to manipulate. So try to take them off.

Russel's paradox: there a type error

Types are usefull to optimize.

## TypeChecking

Determine if an expression is valid. Determine if a type is compatible with another is long to check.

### Strongly typed languages
When we can determine the type of a variable whenever during the running time.

C++ is not strongly typed because of unions.

### Equivalence

### Static typing vs dynamic typing  

static types determined at the compiletime, dynamic determined during runtime.

### Type checking and type infrence

  Begining to type leaves in the AST

***

# 2018-03-12

---

coercision : Conversion narrow / wide conversion

Type of while: void

```
while (not(true = false))
  (
    1 + 2 * 42 - 0;
    8.0
  )
```

## Subtypes

On dénote par la relation X <= Y pour dire:

* X est une sous classe de Y
* X peut s'utiliser là où on peut utiliser Y
* X est conforme à Y (a les mêmes propriétés que)

### Lub (Least Upper Bound)

LUB(X, Y) = Z
X <= Z && Y <= Z
Et
s'il existe Z' tq X <= Z' && Y <= Z' alors Z <= Z'
