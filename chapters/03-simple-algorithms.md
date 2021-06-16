# Simple Algorithms

## Review

### Loops Review

Guess and check for finding square root

```py
ans = 0
neg_flag = False
x = int(input("Enter an integer: "))
if x < 0:
    neg_flag = True
while ans**2 < x:
    ans = ans + 1
if ans**2 == x:
    print("Square root of", x, "is", ans)
else:
    print(x, "is not a perfect square”)
    if neg_flag:
        print("Just checking... did you mean", -x, "?”)
```

### Strings

- sequence of case sensitive characters
- can compare with `==`, `<`, `>` etc. based on lexicographic ordering
- `len()` is used to retrive the **length** of string passed as parameter
- square brackets used to perform **indexing** into a string to get the value at certain index/position
  ```py
  >>> s = "abc"
  >>> len(s)
  3
  >>> s[0]
  'a'
  >>> s[1]
  'b'
  >>> s[3]
  Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  IndexError: string index out of range
  ```

String is indexed from 0.

```
s = "abc"
     012   <-- index
```

- can **slice** strings using `[start:stop:step]`
  ```py
  >>> s = "abcdefgh"
  >>> s[::-1]
  'hgfedcba'
  >>> s[3:6]
  'def'
  >>> s[-1]
  'h'
  ```
- strings are **immutable** - cannot be modified
  ```py
  >>> s = "hello"
  >>> print(s)
  hello
  >>> type(s)
  <class 'str'>
  >>> s[0] = 'y'
  Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  TypeError: 'str' object does not support item assignment
  >>> s = 'y'+s[1:len(s)]
  >>> print(s)
  yello
  ```
  Last command works because `s` is not being modified. Instead, it is being **redefined**.

### `for` loops

- have a loop variable that iterates over a set of values

  ```py
  for var in range(4):
      <expressions>
  ```

  - `var` iterates over values 0,1,2,3
  - expressions inside loop executed with each value for `var`

```py
for var in range(4,8):
<expressions>
```

- `var` iterates over values 4,5,6,7
- `range` is a way to iterate over numbers. `for` loop however can iterate over other items too. Following snippet iterates over characters of a string

  ```py
  s = "abcdefgh"

  for char in s:
      if char == 'i' or char == 'u':
          print("There is an i or u”)
  ```

## Approximate Solutions

- **good enough** solution
- start with a guess and increment by some **small value**
- what is _good enough_?
  ```
  |guess3|-cube <= epsilon
  ```
  - for some small epsilon

```py
cube = 27
epsilon = 0.01
guess = 0.0
increment = 0.0001
num_guesses = 0
while abs(guess**3 - cube) >= epsilon: and guess <= cube :
    guess += increment
    num_guesses += 1
print('num_guesses =', num_guesses)
if abs(guess**3 - cube) >= epsilon:
    print('Failed on cube root of', cube)
else:
    print(guess, 'is close to the cube root of', cube)
```

This code takes lots of iteration to arrive at an answer. For cube root of 27, it takes ~30k iterations.

### Observations

- step could be any small number
  - if epsilon is very large, answer will be inaccurate
  - if epsilon is very small, answer will take lot of time to arrive at
- in general, will take `x/step` iterations to find solution
- we certainly need more efficient way to do this

## Bisection Search

Lets talk with example of square roots

- we know that square root of a number `x` lies between 1 and `x`
- rather than exhaustively trying numbers starting from 1, suppose we instead pick a number in the middle of this range - i.e. `x/2` (or `(x+1)/2` for odd x)
- if we are lucky, this answer will be close engough!
- if not close enough, is guess to small or too large?
- if `guess**2 > x`, then know that `guess` is too large. We can be sure that any number greater than `guess` cannot be the answer. Take the next guess as `guess/2`.
- if `guess**2 < x`, then numbers lesser than `guess` can be discarded. This time, new guess will be `(x+guess)/2`.

With each stage, we are discarding half the value! Here is the complete code for finding square root using bisection search

```py
x = 25
epsilon = 0.01
numGuesses = 0
low = 1.0
high = x
ans = (high + low)/2.0

while abs(ans**2 - x) >= epsilon:
    print('low = ' + str(low) + ' high = ' + str(high) + ' ans = ' + str(ans))
    numGuesses += 1
    if ans**2 < x:
        low = ans
    else:
        high = ans
    ans = (high + low)/2.0
print('numGuesses = ' + str(numGuesses))
print(str(ans) + ' is close to square root of ' + str(x))
```

This code will run in 13 guesses.

Lets do the same thing with cube roots

```py
cube = 27
epsilon = 0.01
num_guesses = 0
low = 1
high = cube
guess = (high + low)/2.0

while abs(guess**3 - cube) >= epsilon:
    if guess**3 < cube :
        low = guess
    else:
        high = guess
    guess = (high + low)/2.0
    num_guesses += 1
print('num_guesses =', num_guesses)
print(guess, 'is close to the cube root of', cube)
```

This runs in 14 guesses, compared to 30k from last section.

### Biscetion Search Convergence

- search space
  - first guess : $N/2$
  - second guess : $N/4$
  - _g_^th^ guess : $N/2^g$
- `guess` converges on the order of $log_2N$ steps
- bisection search works when value of function varies monotonically with input
- code given works only for positive cubes > 1

### Observations

- bisection search radically reduces computation time
- should work on any function that varies monotonically
  - in above example, the function is `g**2`, which grows as `g` grows

## Dealing with `float`

- approximate real numbers
- internally, computer represents numbers in binary, which may not be exact

### Decimal to binary

Keep dividing by 2, and noting down remainders.

```py
if num < 0:
  isNeg = True
  num = abs(num)
else:
  isNeg = False
result = ‘‘
if num == 0:
  result = ‘0’
while num > 0:
  result = str(num%2) + result
  num = num//2
if isNeg:
  result = ‘-’ + result
```

### Fractions and binary

- if there is no integer `p` such that `x*(2**p)` is a whole number, then internal representation is always an approximation
- test equality of `float`s by using `abs(x-y)<e` where `e` is a small number, rather than using `x==y`

## Newton Raphson

- general approximation algorithm to find roots of a polynomial in one variable

  $p(x) = a_nx^n + a_{n-1}x^{n-1} + ... + a_1x + a_0$

- we want to find $r$ such that $p(r) = 0$
- for example, to find the square root of 24, find the root of $p(x) = x^2 - 24$
- Newton showed that if $g$ is an approximation to the root, then

  $g - p(g)/p\prime(g)$

  is a better approximation; where $p\prime$ is derivative of $p$.

```py
epsilon = 0.01
y = 24.0
guess = y/2.0
numGuesses = 0

while abs(guess*guess - y) >= epsilon:
  numGuesses += 1
  guess = guess - (((guess**2) - y)/(2*guess))
print(‘numGuesses = ‘ + str(numGuesses))
print('Square root of ' + str(y) + ' is about ' + str(guess))
```
