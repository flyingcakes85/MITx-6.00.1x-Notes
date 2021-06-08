# Introduction to Programming

## Knowledge

- **Declarative knowledge** is _statement of fact_. Need not tell us how to _achieve_ a task. Eg - "There is a candy under one of the chairs." Tells us a fact, but does not give any process to _find_ that candy.
- **Imperative knowledge** is a _recipe_ or "how-to" process for a task. In the above example, we could have said - walk up the third row, until second last chair. Candy is underneath it.

Both are important to us, but only declerative knowledge can be of any value.

### Numerical Example

**Declarative knowledge** : square root of a number $x$ is $y$ such that $y*y = x$. This fact is useful for sure, but doesn't really help us find something.

**Imperative knowledge** : a recipe to find the square root of a number $x$.

1. Start with a _guess_ $g$.
2. If $g*g$ is _close enough_ to $x$, stop and say $g$ is the answer.
3. Otherwise make a _new guess_ by averaging $g$ and $x/g$.
4. Using the new guess, _repeat_ precess until close enough.

Example run for a $x=16$.

| g      | g\*g    | x/g   | (g+x/g)/2 |
| ------ | ------- | ----- | --------- |
| 3      | 9       | 5.333 | 4.1667    |
| 4.1667 | 17.36   | 3.837 | 4.0035    |
| 4.0035 | 16.0277 | 3.997 | 4.000002  |

**Digression** : The above process is said to have been put forth by Heron of Alexandria. It provides a way to calculate _approximate_ square roots. This can be very useful when you don't have access to a calculator and need to calculate root of a non perfect square.

### What is a recipe?

1.  sequence of simple _steps_
2.  _flow of control_ process that specifies when each step is executed
3.  a means of determining _when to stop_

## Computers are machines

- **Fixed program** computer : made for only a specific task. Eg. handheld calculator, Alan Turing's Bombe.
- **Stored program** computer : can do different tasks by emulating multiple fixed program computers.

### Basic machine architecture

- **Memory** - stores data or sequence of instructions that a program requires to run
- **Arithmetic Logic Unit** (ALU) - takes information from memory, reads it and perform a primitive operation (like addition, check for truth etc)
  **Control Unit** - keeps track of the operations we are doing in ALU at a point of time. It also has a program counter. When we first load a program, its instructions are loaded in memory. Program counter points to this location in memory. When program is executed, it executes the first instruction, and increses the counter by 1. At tests, the program counter my be changed to a number not necessarily that comes after it. This happens when the executions needs to jump to a statement in different part of the memory.

### Stored program computer

A sequence of **instructions** stored inside computer built from predefined set of primitive instructions.

- arithmetic and logic
- simple tests
- moving data

A special program - the **interpreter** - executes each instruction in order.

- use tests to change flow of control through sequence
- stop when done

### Basic Primitives

Most machines comes with simple arithmetic logic. However, Turing showed that you can compute anything using 6 primitives.

- Right: Move the machine’s head to the right of the current square
- Left: Move the machine’s head to the left of the current square
- Print: Print a symbol on the current square
- Scan: Identify any symbols on the current square
- Erase: Erase any symbols presented on the current square
- Nothing/halt: Do nothing

Programming using these primitives can get very tedious. Modern programming languages come with a more convinient set of primitives. They can also **abstract** a set of instructions to _create a new primitive_.

There is a fundamental property, that _anything computable in one programming language is computable in other programming language_. This property is called Turing complete. However, for achieving a given task, one language may be easier than other.

## Programming Languages

- a programming language provides a set of primitive **operations**
- **expressions** are complex but legal combination of primitives in a programming language
- expressions and computations have **values** and meanings in a programming language

### Aspects of language

1. **primitive constructs** : numbers, strings, simple operations; quite like the role words play in English
2. **syntax** : correct ordering of different words in English; in programmming languages, too, primitive constructs need to follow certain grammar
3. **static semantics** : syntactically valid strings have meaning
   - `3.2*5` \rightarrow semantically valid
   - `3+"hi"` \rightarrow static semantic error
4. **semantics** : is the meaning associated with a syntactically correct string of symbols with no static semantic errors. In programming languages, a semantically correct statement can have only one meaning, but may not be what the programmer intended

### Errors

1. **syntactic error**
   - common and easily caught
   - most compilers or environments will catch them
2. **static semantic error**
   - some languages check for these before running the program
   - some langauges (like Python), will do this on the fly while running the program
   - can cause unpredictable behaviour
3. no semantic errors, but _different meaning than what programmer intended_
   - program crashes; stops running
   - program runs forever
   - program runs, but output isn't what you expected

## Python programs

- a program is a sequence of definitions and commands
  - definitions are **evalueted**
  - commands are **executed** by Python interpreter in a **shell**
- **commands** (statements) instruct interpreter to do something
- commands can be typed directly in a shell or stored in a **file** that is read into the shell and executed

### Objects

- programs manipulate **data objects**
- objects have a **type** that defines the kinds of things programs can do to them
- objects are one of the follows
  - _scalar_ \rightarrow cannot be subdivided
  - _non-scalar_ \rightarrow have internal structure that can be accessed

### Scalar objects

- `int` - represent **integers**, i.e. numbers without a fractional part
- `float` - represent **real numbers**
- `bool` - represent **Booloan** values `True` and `False`
- `NoneType` - **special**, has one value - Null

### Python shell

Can be accessed by typing `python3` or similar in the terminal. (depends on your distribution)

It gives the following output

```
Python 3.9.5 (default, May 24 2021, 12:50:35)
[GCC 11.1.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Here you can type Python statements that will be interpreted and their output displayed.

#### Printing data

```py
>>> print(4+2)
6
```

#### Knowing types

```py
>>> type(3)
<class 'int'>
>>> type(4.6)
<class 'float'>
```

### Type casting

Can change objects from one type to another.

```py
>>> float(4)
4.0
>>> int(4.93)
4
```

Point to note : `int()` doesn't round off to the nearest integer. Instead, it just drops off the fractional part.

### Expressions

- **combine objects and operators** to form expressions
- an expression has a **value** which has a type
- basic syntax:

```
<object> <operator> <object>
```

### Operators on `int` and `float`

| Expression | Meaning                          |
| :--------: | -------------------------------- |
|   `i+j`    | sum                              |
|   `i-j`    | difference                       |
|   `i*j`    | product                          |
|   `i/j`    | division (float)                 |
|   `i//j`   | int division (quotient only)     |
|   `i%j`    | remainder when i is divided by j |
|   `i**j`   | i to power of j                  |

```py
>>> 4+6
10
>>> 5/2
2.5
>>> 5//2
2
>>> 17%4
1
>>> 4**5
1024
```

### Operator precedence

- parenthesis tell Python to evalate the enclosed expression first
  - `3*5+1` evaluates to 16
  - `3*(5+1)` evaluates to 18
- **operator precedence** without parenthesis (top to down)
  - `**`
  - `*` and `/`
  - `+` and `-`
  - executed left to right, as appear in expression

## Variables

- equal sign is an **assignment** of a value to a variable

```py
pi = 3.14159
pi_approx = 22/7
```

- value is stored in computer memory
- an assignment _binds_ name to value
- value associated with a name or variable can be retrieved by invoking the name, for example `pi`
- these names can be used later in your program

```py
>>> pi = 3.14159
>>> pi
3.14159
>>> pi + 2
5.14159
```

## Abstracting expressions

Why give names to values of expression? Because it lets us reuse names instead of values. This makes easier to change code later on.

```py
pi = 3.14159
radius = 2.2
area = pi*(radius**2)
```

## Programming v/s Maths

_We are not solving for 'x'!_

An expression with equal sign is not meant to be solved for a variable. Instead, it means that the value on right side of equal sign should be assigned to the variable on left of equal sign.

## Changing bindings

A variable can be assigned a new value later on in the program. Also, when a variable changes value, other variables which used it before don't change values. Previous value may still be stored in memory, but the handle to it is lost. Consider example below

```py
pi = 3.14159
radius = 2.2
area = pi*(radius**2)
radius = radius+1
```

In the last statment, `radius` is increased by 1. But the value of `area` does not change with this increment. Programming languages only follow the statements provided to them.

## Operators and Branching

### Comparision operators on `int` and `float`

- `i` and `j` are any variable names
  - `i > j`
  - `i >= j`
  - `i < j`
  - `i <= j`
  - `i == j` \rightarrow **equality test**, `True` if `i` equals `j`
  - `i != j` \rightarrow **inequality test**, `True` if `i` not equal to `j`

### Logical Operators on `bool`

- `a` and `b` are any variable names
  - `not a` \rightarrow
    - `True` if `a` is `False`
    - `False` if `a` is `True`
  - `a and b` \rightarrow `True` if both are `True`
  - `a or b` \rightarrow `True` if either or both are `True`

### Branching Programs

The simplest branching statement is a **conditional**. The components are

1. a test (expression that evaluates to `True` or `False`)
2. a block of code to execute if the test is `True`
3. an optional block of code to execute if the test is `False`

The third component, for `False` block, is optional in Python, but the second component is compulsury.

```py
x = int(input('Enter an integer: '))
if x%2 == 0: # test
  print('')      #
  print('Even')  # block 1 (True)
else:
  print('')      #
  print('Odd')   # block 2 (False)
print('Done with conditional')
```

The expression `x%2 == 0` evaluates to `True` when the remainder of `x` divided by 2 is 0. The indentation is important - each indented set of expressions denote a block of instructions.

### Nested conditionals

```py
if x%2 == 0:
  if x%3 == 0:
    print('Divisible by 2 and 3’)
  else:
    print('Divisible by 2 and not by 3’)
elif x%3 == 0:
  print('Divisible by 3 and not by 2’)
```

`elif` is shorthand for else if. Provides extra conditions for `if` branching.

### `=` v/s `==`

Equal sign binds value to a variable. Double equals compares two values and returns a boolean.

## Conclusion

We have studied basic syntax of Python. We can now branch our program. Still, each statement in our program will get executed at most once. Therefore, the maximum time to run the program depends only on the length of the program. We can say our programs run in **linear time**.
