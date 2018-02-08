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

a+b est-il valide?
&emsp;-> Liaison de nom (savoir où sont définies les variables)  

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
&emsp;-> We chose the ML bool. Modern compiler implementation in ML

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
&emsp;-> Create module and create a function `print(exp)` outside the class.

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

`` xalloc `` can add parameters to ``<<`` operator

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
