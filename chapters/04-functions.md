# Funcions

## Good Programming

- more code not necessarily a good thing
- measure good programmers by the amount of functionality
- introduce **functions**
- mechanism to achieve **decomposition** and **abstraction**

### Example - projector

- a projector is a black box
- don't know how it works
- know the interface : input/output
- connect any electronics to in that can communticate with that input
- black box somehow converts image from input source to a wall, magnifying it
- **ABSTRACTION IDEA** : do not need to know how a projector works to use it
- projecting large images decomposed into separate tasks for separate projectors
- each projector takes input and produces separate output
- all projectors owrk together to produce larger image
- **DECOMPOSITION IDEA** : different devices work together to achieve an end goal

### Applying these idea to programming

- Decomposition: Break problem into different, self-contained pieces

- Abstraction: Supress details of method to compute something from use of that computaiton

## Create Structure with Decomposition

- divide code into **modules**
  - are **self-contained**
  - used to break up code
  - intendede to be reusable
  - keep code organized
  - keep code coherent
- we can achieve decomposition with **functions** or **classes**

## Suppress Details with Abstraction

- think of a piece of code as a **black bok**
  - cannot see details
  - do not need to see details
  - do not want to see details
  - hide tedious coding details
- achieve abstraction with **function specifications** or **docstrings**

## Writing Functions

- write reusable pieces/chunks of code, called **funciton**
- functions are not run ina a program unless they are **called** or **invoked**
- function characters
  - has a **name**
  - has **parameters** (0 or more)
  - has a **docstring** (optional but recommended)
  - has a **body**

### Example

```py
def is_even( i ):
    """
    Input: i, a positive int
    Returns True if i is even, otherwise False
    """
    return i%2 == 0

is_even(3)
```

Here, `is_even` is the function name. `( i )` is parameter list. Next, the text enclosed between `"""` is called docstring. At the end, `is_even(3)` is function invocation. It passes the number 3 as value of `i`. In the function, wherever `i` appears, it will be replaced with 3. The `return` keyword defines the value to be given back. In this case, it calculates remainder when `i` is divided by 2, and if its 1, meaning `i` is odd, then `False` is returned. For even `i`, `i%2` is 0, and `True` is returned.

## Variable Scope

- **formal parameter** gets bound to the value of **actual paramater** when function is called
- new **scope/ frame/ evironment** created when we enter a function
- **scope** is mapping of names to objects

```py
def f( x ):
    x = x + 1
    print('in f(x): x=', x)
    return x

x = 3
z = f(x)
```

Function `f(x)` also has the variable `x`, but it does' not conflict with the variable `x` defined below. This is because the variable in `f(x)` is in function scope. The other variable `x` defined below is in the global scope. Scopes are like different environments or frames. Value of variables used in a frame is relative to that frame.

- inside a funciton, can access a variable defined outside
- inside a function, cannot modify a variable defined outside

## Functions as Arguments

- arguments can take any type - even functions

```py
def func_a():
    print('inside func_a')
def func_b(y):
    print('inside func_b')
    return y
def func_c(z):
    print('inside func_c')
    return z()

print(func_a())
print(5+func_b(2))
print(func_c(func_a))
```

## Default Arguments Values

Can specify that some arguments have default values, so if no value is supplied, just use the default value

```py
def printName(firstName, lastName, reverse = False)
    if reverse:
        print(lastName + ', ' + firstName)
    else:
        print(firstName, lastName)

printName('Hello', 'World') # will use default value False for reverse
printName('Hello', 'World', True)
```

## Specifications

- a contract between the implementer of a function and the clients who will use it
  - **Assumption**: conditions that must be met by clients of the function; typically constraints on values of parameters
  - **Guarantee**: contitions that must be met by funciton, providing it has been called in manner consistent with assumptions

We can achieve this with **docstrings**;

```py
def is_even( i ):
    """
    Input: i, a positive int #assupmtion
    Returns True if i is even, otherwise False #guarantee
    """
    return i%2 == 0

is_even(3)
```

## Recursion and Iteration

### Iteration

- looping constructs lead to iterative algorithms
- can capture computations in a set of state variables that update on each iteration through loop

Example

```py
def mult_iter(a, b):
    result = 0
    while b > 0:
        result += a
        b -= 1
    return result
```

### Recursion

- way to design solution by divide and conquer
- a programming technique where a function calls itself
- in programming, goal is to NOT have infinite recursion
  - must have one of more base cases that are easy to solve
  - must solve the same problem on some other input with the goal of simplifyinng larger problem input

Example

```py
def mult(a, b):
    if(b == 1):
        return a
    else:
        return a + mult(a, b-1)
```

### Computing Factorial

- base case
  ```py
  if n == 1:
      return 1
  ```
- higher cases \rightarrow reduce problem
  $n! = n * (n - 1)!$
  ```py
  else:
      return n*factorial(n-1)
  ```

### Observations

- each recursive call to a function creates its own scope/environment
- bindings of variables in a scope is not changed by recursive call
- flow of control passes back to previous scope once function call returns value
- recursion may be simpler, more intuitive
- recursion may be efficient from programmer POV
- recursion may not be efficient from computer POV

## Inductive Reasoning

To prove a statement indexed on integers is true for all values of `n`:

- Prove it is nrue when `n` is smallest (eg. `n=0` or `n=1`)
- Then prove that if it is true for an arbitrary value of `n`, one can show that it must be trou for `n+1`

Induction can help us verify correctness of recursive algorithms.

## Towers of Hanoi

There are three stacks, one with discs in increasing size from top to bottom, and other two are empty. Objective is to move the discs from one stack to another, without ever having a larger disc above smaller disc in any intermediate step.

This can be easily solved by using recursion. Moving a stack of 1 disc is the base case. Larger cases can be broken down.

```py
def printMove(fr, to):
  print('move from ' + str(fr) + ' to ' + str(to))


def Towers(n, fr, to, spare):
  if n == 1:
    printMove(fr, to)
  else:
    Towers(n-1, fr, spare, to)
    Towers(1, fr, to, spare)
    Towers(n-1, spare, to, fr)
```

## Fibonacci Numbers

$1 1 2 3 5 8 13 21...$

```py
def fix(x):
  if x == 0 or x == 1:
    return 1
  else:
    return fix(x-1) + fix(x-2)
```

## Palindrome

- Convert string to just characters, by stripping out punctuation and converting upper case to lower case
- Then
  - Base case: a string of length 0 or 1 is a palindrome
  - Recursive case: if first character matches last character, then it is a palindrome if middile section is palindrome

```py
def isPalindrome(s):
  def toChars(s):
    s = s.lower()
    ans = ''
    for c in s:
      if c in 'abcdefghijklmnopqrstuvwxyz':
        ans = ans + c
      return ans

    def isPal(s):
      if len(s) <= 1:
        return True
      else:
        return s[0] == s[1] and isPal(s[1:-1])

    return isPal(toChars(s))
```

## Divide and Conquer

- Checking for palindrome using recursion is an example of divide and conquer algorigthm
- solve a hard problem by breaking it into a set of sub-problems such that:
  - sub-problems are easier to solve than the original
  - solutions of the sub-problem can be combined to solve the original

## Modules and Files

- storing all our code in one file is cumbersome for large projects
- **module** is a `.py` file containing a collection of Python definitions and statements

```py
# circle.py

pi = 3.14159

def area(radius):
  return pi*(radius**2)

def circumference(radius):
  return 2*pi*radius
```

```py
# code.py

import circle
pi = 3
print(pi)
print(circle.pi)
print(circle.area(3))
print(circle.circumference(3))
```

Results:

```
3
3.14159
28.27431
18.849539999999998
```

If we don't want to refer to funciton variables by their module and the names don't collide with other bindings, we can use following syntax:

```py
from circle import *
print(pi)
print(area(3))
```

Now, we don't need to prepend `circle.` before any function or variable reference.

## File Handling

- need a way to save work for later use
- access files using a **file handler**
  ```py
  nameHandle = open("myFile", 'w')
  ```
  This creates a file named `myFile` and returns a file handle. The `'w'` indicates the file is opened for writing into.

### Writing

```py
nameHandle = open('myFile', 'w')
for i in range(2):
  name = input('Enter name: ')
  nameHandle.write(name + '\n')
nameHandle.close()
```

### Reading

```py
nameHandle = open('myFile', 'r')
for line in nameHandle:
  print(line)
nameHandle.close()
```
