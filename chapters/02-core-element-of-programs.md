# Core Elements of Programs

## Example - Swapping Numbers

### With an extra variable

```py
x = 1
y = 2
temp = y
y = x
x = temp
```

### Without extra variable

```py
x = 1
y = 2
x = x + y
y = x - y
x = x - y
```

This approach will not work for very large numbers, as you risk overflow at the line `x = x + y`.

## Strings

- It is a sequence of lettrs, special characters, spaces or digits
- They are enclosed in quotation marks or single quotes
  ```py
  hi = "hello there"
  greeting = "hello"
  ```
- **concatenate** strings
  ```py
  name = "snehit"
  greet = hi + name
  greeting = hi + " " + name
  ```
  The addition operator here works differently than how it works with `int` or `float`. It can be weird to think about _adding_ strings like numbers, however, they do have a natural manner of getting combined, that is to take the two strings and joint it. Plus symbol when used with strings perform this concatenation. This is called operator overloading - the same operator behaves differently when used with different types.
  Concatenation using plus symbol does not put space between the two strings.

## Operations on Strings

- `'ab' + 'cd'` \rightarrow string **concatenation**
- `3* \'snehit\'` \rightarrow string **successive concatenation**
- `len('snehit')` \rightarrow string **length**
- `'snehit'[1]` \rightarrow string **indexing**
- `'snehit'[1:3]` \rightarrow string **slicing**

```py
>>> 3*'snehit'
'snehitsnehitsnehit'
>>> len('snehit')
6
>>> 'snehit'[1]
'n'
>>> 'snehit'[0]
's'
>>> name = 'snehit'
>>> name[0]
's'
>>> 'snehit'[6]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
>>> 'snehit'[1:5]
'nehi'
>>> 'snehit'[:3]
'sne'
>>> 'snehit'[1:]
'nehit'
>>> 'snehit'[:]
'snehit'
```

## Input/Output

### `print`

Used to **output** text to console.

```py
>>> x = 1
>>> print(x)
1
>>> x_str = str(x)
>>> print("my fav num is", x, ".", "x =", x)
my fav num is 1 . x = 1
>>> print("my fav num is " + x_str + ". " + "x = " + x_str)
my fav num is 1. x = 1
```

### `input`

- prints the string provided in quotes
- user types an input and presses enter
- returns the inputted value
- this return value is bound to a variable
  ```py
  >>> text = input("Type anything... ")
  Type anything... Hello
  >>> print(5*text)
  HelloHelloHelloHelloHello
  ```
- returns string to need to type cast before storing numbers
  ```py
  >>> num = int(input("Type a number... "))
  Type a number... 35
  >>> print(5*num)
  175
  ```

## While loop

- lets you repeatedly execute a set of statements
- syntax
  ```py
  while <conditions>:
    <expression>
    <expression>
  ```
  - `<condition>` evaluates to a Boolean
  - if `<condition>` is `True`, do all the steps inside the while code block
  - check `<condition>` again
  - repeat until `<condition>` is false

Example

```py
n = 0
while n < 5:
  print(n)
  n = n + 1
```

Output

```
0
1
2
3
4
```

If you forget putting the increment `n=n+1` in the above code, the program will run infinitely, printing zero.

## For loop

- syntax
  ```py
  for <variable> in range(<number>):
    <expression>
    <expression>
  ```
  - each time through the loop, `<variable>` takes a value
  - first time, `<variable>` starts at the smallest value
  - next time, `<variable>` gets the previous value + 1
  - repeat

Example

```py
for n in range (5):
  print(n)
```

This snippet prints the same output as the earlier one. `range(x)` gives a list of integers starting from 0 to `x-1`.

### `range`

For `range`, default `start` value is 0, `step` value is 1. Loops until `stop-1`.

- custom `start` value
  ```py
  mysum = 0
  for i in range(7, 10):
    mysum += i
  print(mysum) # 24
  ```
- custom `step` value
  ```py
  mysum = 0
  for i in range(5, 11, 2):
    mysum += i
  print(mysum) # 21
  ```

## `break`

- immediately exits whatever loop it is in
- skips remaining exrpessions in code blocks
- exits only innermost loop

```py
while <condition 1>:
  while <condition 2>:
    <expression a>
    break
    <expression b>
  <expression c>
```

Here, `exrpession b` is never executed, because `break` exits out of the inner loop before that. `expression a` is executed, then `expression c`.

```py
mysum = 0
for i in range(5, 11, 2):
  mysum += 5
  if mysum == 5:
    break
print (mysum)
```

This code prints `5`. At that value of `mysum`, the loop breaks.

## `for` v/s `while` loop

- `for` loops know the number of iterations before hand. `while` loops have unbounded number of iterations.
- Both can end early via `break` statement
- `for` loop uses a counter to keep track of iterations. `while` loop can also use a counter, but it must be initialized before the loop and be incremented inside the loop
- `for` loop can be rewritten using a `while` loop, however, the revers may not be always possible

## Guess and Check

One of the ways to solve a problem

- guess a value for the solution
- check if the guess is correct
- keep guessing until you find the solution or guesses all possible values

This process is _exhaustive eumeration_.
