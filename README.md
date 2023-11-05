![Jaffna Logo](./res/white.png)

<center>
    <h1>Jaffna</h1>
    <h3>When math meets programming.</h3>
</center>

Jaffna is a programming language with the aim of being as close to mathematical expressions as possible. This is being done with the following aims:

* Learning purposes (mostly for students) so that programming is being made easier by building analogies to mathematics.

* Besides learning application in the real world for calculations and even proofs.

* Enabling a wider range of people to do calculations based on an already known concept.

This document is an entire documentation of the Jaffna language and provides besides code examples and technical information and the philosophies and thoughts behind the language in order to understand concepts, which are being brought into Jaffna.

## Table of contents

- [Common Concepts](#common-concepts)
    - [Variables](#variables)
    - [Sets](#sets)
    - [Conditional logic](#conditional-logic)
    - [Loops](#loops)
    - [Functions](#functions)
    - [Comments](#comments)
- [Data Structures](#data-structures)
- [Modules](#modules)
    - [In-built modules](#in-built-modules)
        - [std module](#std-module)
        - [io module](#io-module)
        - [set module](#set-module)
        - [seq module](#seq-module)

## Common concepts
There are some concepts, which are present in all languages and so are they also in Jaffna. Although their approach is different.

### Variables
Variables in Jaffna are declared by their name following the type. Here is a little example.

```
x: int = 10
```

However it is not mandatory for the variable to also be defined. So something like

```
x: int
```

is also valid.

### Sets
Jaffna has the concept of everything being a set ("Everything is a set"). Predefined types are

#### Numerical sets

* nat: Natural numbers
* int: Integers
* rat: Rational numbers
* real: Real numbers

#### Other sets

* bool: Boolean values
* char: Characters
* string: Strings (A sequence of characters)
* nil: The empty set

The reason why Jaffna takes this approach is that variables and even functions are always associated with sets and since Jaffna aims to be as close to mathematics as possible this concept is a step in order to get closer to that.

It is possible to define own sets.<br>
Let's for example create a set of dogs. In Jaffna this would look like this.

```
set Dog = {(name, age, race) | name: string, age: nat, race: string}
```

In other programming languages the kind of equivalent would be a so-called type.

Now let's use our new set for declaring a variable:

```
dog1: Dog = ("Bob", 12, "Border Collie")
```

After declaring this variable the Jaffna interpreter will make sure that the element is adhering to the conditions of the set. If it doesn't the respective error will be raised.

Besides that sets can also be used to store data. However sets are not able to store duplicate values. The usage of Sets as a data structure is decribed [here](#sets-as-data-structures).

### Conditional logic
Since we have also boolean values as an in-built set it is possible to have conditional logic in Jaffna:

```
if(x == 0)
    x = x+3
else
    x=x+1
endif
```

### Loops
Like other languages Jaffna also offers loops such as the while loop:

```
while(x!=0)
    x = x+1
endwhile
```

Or the for loop:

```
for(x: nat = 0, x < 10, x = x+1)
    y = x+1
endfor
```

### Functions

Like any other programming language, Jaffna also provides functions. There are two types of functions Jaffna has:

* [Typical functions](#typical-functions)
* [Anonymous/Lambda functions](#anonymouslambda-functions)

#### Typical functions
A typical function is like in math a relation between two sets and is declared in Jaffna in the following way:

```
fn parabola(x): (int->int)
    return x*x
endfn 
```

We are first using the fn keyword in order to tell the interpreter that we want to declare a function. After that we provide the name and declare the function parameters followed by the function type, which defines the domain and the range of the function.

Now in other programming languages there are also functions which are not returning anything (a so called "procedure"). This is being solved in Jaffna by declaring a function which uses the empty set as the range of the function. Here is an example of this.

```
import io

fn greeting(name): (string->nil)
    io.print("Hello " + name)
endfn
```

It's also possible to have functions without a parameter:

```
import io

fn helloWorld(): (nil->nil)
    io.print("Hello world!")
endfn
```

#### Anonymous/Lambda functions
In Jaffna it is also possible to declare anonymous or so called lambda function. Let's take our Hello World function from our previous example and write it as a lambda function:

```
import io

helloWorld: (nil->nil) = ()=>(io.print("Hello World!"))
```

### Comments
Adding commands to your Jaffna code is pretty straight forward. You can have single-line comments:

```
//This is a single line comment.
```

And also multi-line comments:
```
/*
    This is a multiline comment.
*/
```

## Data Structures
Like any other programming language it is also possible to store chunks of data in data structures. Jaffna provides the following ones:
- [Sets](#sets-as-data-structures)
- [Sequences](#sequences)

### Sets as data structures
Like in maths, sets can also be used to store data. However unlike other data structures some of you are familiar with, the set does not allow duplicate values or being sorted in the first place since it otherwise would go against the mathematical definition of a set.

Let's declare such a set:

```
x: set<int> = {1, 30, 15, 12} 
```

In order to access data from a set, you have to apply a filter to the set so that you get the desired values.

```
y = set.filter(x,(a)=>(a==1))
```

However if you want to get your data by an index you have to make a countable set:

```
l: c_set<int> = {1, 55, 13, 12}
m = c_set[2]
```

In order to append an element to a set you use:

```
set.append(l, 3)
```



### Sequences

The sequence is comparable to the mathematical object of a sequence and is the equivalent of an array in other languages. Since Jaffna has the "All set" concept, sequences are being realised in the following way:

```
set seq<T> = {(x,y) | x: nat, y: T}
```

So technically you can declare a sequence in the following way:

```
a: seq<int> = {(1, 42), (2, 69), (3,15)}
```

However since this is A) a pain in the ass and B) not very close the mathematical notation of sequences there is a shortcut for it:

```
a: seq<int> = [42, 69, 15]
```
This might look familiar to a few as it is resembling to a so called array. In generall this can be interpreted as such, however sequences do not have a fixed size and are dynamically growing.

In order to access elements from a sequence you can just do the following:

```
f = a[0]
```

## Modules
Modules are ways to further structure your code and make it easier to use (especially when using in projects). A module can be declared in the following way

```
myMod.jf
========
mod myMod

pi: real = 3.1412

fn test(): (nil->nil)
    2+3
end

endmod
```

The import goes as follows:

```
import myMod from 'myMod.jf'

myMod.test()
```

IMPORTANT: Only elements declared inside the mod section are usuable when importing.

### In-built modules
Jaffna already comes with some in-built libraries, which are always being maintained and developed further. These are the current in-built modules.

#### std module

The standard module contains some utility functions, which can be useful. Curretly it contains some mathematical formulas for the everyday calculations. The declaration of the std module can be found in [this file](./std/std.jf).

#### io module

The IO module contains utilies for:
* Interacting with the stdout, stdin and stderr streams
* File handling
* Networking functionality

The declaration for this module can be found in [io.jf](./io/io.jf)

#### set module
The set module contains all the functions needed in order to handle functions that includes:
* appending
* removing
* filtering

The declaration for this module can be found in [here](./collections/set.jf)

#### seq module
The seq module contains all the functions needed for handling sequences. You can look at the seq module code in [seq.jf.](./collections/seq.jf) 