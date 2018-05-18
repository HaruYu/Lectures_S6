---
title: Compilation 2
author: trinh_v
...

# Intermediate Representations

We've checked the semantics, and then the types. Now, we can create an
intermediate language. Thus, we have to handle memory management (with recursive calls.)

Vectorial regiter : super register composed of registers that are "appended"

## Mid end

### Problem

One can do a compiler for every languages. That means a compiler for each
souce to destination

### Solution

One inntermediate language  source $\rightarrow$ inter, inter $\rightarrow$ dest

Multiply it go get as easy as possible (a lot of compilators)

> Intermediate language design is largely an art, not a science.
>> Muchnick, 1997.

## Tree : intermediate language

sxp: executes an instruction for the side effects

## Memory management

- Retisters
- L1 cache, 2-3 cycles
- L2 cache, 10 cycles
- Memory, 100 cycles
- Disks > 1Mcycles

### Activaction blocks

```cpp
fact(3)
fact(2)
fact(1)
fact(0)
```

Each facts are activation blocks. Each fact called are activated.
There is a norm to push the arguments and variables on the stack by the creator
of the processor.

sp : stack pointer (limit between known and unknown part)
fp : frame pointer (begining of the current stack frame)


### Flexible automatic memory

```
int open2(char* str1, char* str2, int flags, int mode){
  char name[strlen(str1) + strlen(str2) + 1];
  stpcpy(stpcpy(name, str1), str2);
  return open(name, flags, mode);
}
```

A problem in CPP because when an exception is thrown, the we don't know the size
 of the stakframe.

$\rightarrow$ using malloc can be a replacement, but the problem is that we have
 to free it.

$\rightarrow$ ``alloca``

When alloca is called, there's gonne be a problem. When it is called, a new
 stacframe is created. and returns to the main function.

> alloca is not a function. Its behaviour is not the same as the functions, so it
> works.

### Nonlocal variables

#### Escaped variables

Go up on the stack stackframe by stackframe to get the escaped variable.

## Static link

Getting a pointer to the previous stackframe. For recursive calls, give the same
stack pointer to the recursive call instead of itself.

### problem

The problem "how many recursive calls" is solved because the pointer of the syntaxic
 parent is given. If the called function calls its "brother", it has to give its
 syntaxic parent.

## Translation to intermediate language

* Preserve some registers (fp sp)
* Allocate frames
* handle static link
* Receive  the arguments

prototranslation: Translate as much as possible before returning to the parent.

```
Cjump e T, F
label F
  Cjump !e, F, T
  label T
    Cjump e, T, F
    jump F
```


# 14-05-2028

* On ne peut pas compiler en étant le plus optimal possible. Il faut faire des
choix.

# Liveness Analysis

On a un pseudo assembleur avec des registres limité. On doit savoir quand nait
une variable et quand elle meurt.

Exemple:

```
  t0 = 1
  t1 = 2
L1: t2 = t0 + t0
  t1 = t1 * t2
  if t1 < t3 goto L1
  return t1
```
