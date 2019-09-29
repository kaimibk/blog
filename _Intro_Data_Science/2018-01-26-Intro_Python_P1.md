---
layout: post
title:  "Introduction to Programming with Python"
categories: posts
date:   2018-01-26 12:00:00 -1000
---

# Introduction to Programming

## What does a computer do?

1. Executes commands in sequence
2. Each command operates on the current state of the machine

**Remember:** Computers are dumb

## What does code do?

Code is nothing more than a stored sequence of commands carried out by the computer.

![alt text](https://imgs.xkcd.com/comics/ai_research_2x.png)


# Standalone Python Topics

## Functions

We will start by introducing two fundamental functions in Python:
1. `print()`
2. `help()`

### Print Function
As the name implies, this function prints whatever you tell it to. For example,


```python
print('Hello World')
print(5)
```

    Hello World
    5


`print()` can take multiple parameters:


```python
print('Hello', 'World')
print(4, 2, sep='*')
```

    Hello World
    4*2


### Exercise
Use the print function to print your name and age

**Solution:**


```python
print('your name and age')
```

    your name and age


### Help Function
This function will tell how how to use a certain function, and what parameters it takes.


```python
help(print)
```

    Help on built-in function print in module builtins:
    
    print(...)
        print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
        
        Prints the values to a stream, or to sys.stdout by default.
        Optional keyword arguments:
        file:  a file-like object (stream); defaults to the current sys.stdout.
        sep:   string inserted between values, default a space.
        end:   string appended after the last value, default a newline.
        flush: whether to forcibly flush the stream.
    


### Exercise

There are many built-in functions available in Python 3.6, for a list see [here.](https://docs.python.org/2/library/functions.html)

Use the help function to check the following built in functions:
1. `list`
1. `sum`
1. `min`

**Solution:**


```python
# Number 1
help(list())

# Number 2
help(sum)

# Number 3
help(min)
```

    Help on list object:
    
    class list(object)
     |  list(iterable=(), /)
     |  
     |  Built-in mutable sequence.
     |  
     |  If no argument is given, the constructor creates a new empty list.
     |  The argument must be an iterable if specified.
     |  
     |  Methods defined here:
     |  
     |  __add__(self, value, /)
     |      Return self+value.
     |  
     |  __contains__(self, key, /)
     |      Return key in self.
     |  
     |  __delitem__(self, key, /)
     |      Delete self[key].
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getitem__(...)
     |      x.__getitem__(y) <==> x[y]
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __iadd__(self, value, /)
     |      Implement self+=value.
     |  
     |  __imul__(self, value, /)
     |      Implement self*=value.
     |  
     |  __init__(self, /, *args, **kwargs)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __len__(self, /)
     |      Return len(self).
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __mul__(self, value, /)
     |      Return self*value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __reversed__(self, /)
     |      Return a reverse iterator over the list.
     |  
     |  __rmul__(self, value, /)
     |      Return value*self.
     |  
     |  __setitem__(self, key, value, /)
     |      Set self[key] to value.
     |  
     |  __sizeof__(self, /)
     |      Return the size of the list in memory, in bytes.
     |  
     |  append(self, object, /)
     |      Append object to the end of the list.
     |  
     |  clear(self, /)
     |      Remove all items from list.
     |  
     |  copy(self, /)
     |      Return a shallow copy of the list.
     |  
     |  count(self, value, /)
     |      Return number of occurrences of value.
     |  
     |  extend(self, iterable, /)
     |      Extend list by appending elements from the iterable.
     |  
     |  index(self, value, start=0, stop=9223372036854775807, /)
     |      Return first index of value.
     |      
     |      Raises ValueError if the value is not present.
     |  
     |  insert(self, index, object, /)
     |      Insert object before index.
     |  
     |  pop(self, index=-1, /)
     |      Remove and return item at index (default last).
     |      
     |      Raises IndexError if list is empty or index is out of range.
     |  
     |  remove(self, value, /)
     |      Remove first occurrence of value.
     |      
     |      Raises ValueError if the value is not present.
     |  
     |  reverse(self, /)
     |      Reverse *IN PLACE*.
     |  
     |  sort(self, /, *, key=None, reverse=False)
     |      Stable sort *IN PLACE*.
     |  
     |  ----------------------------------------------------------------------
     |  Static methods defined here:
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |  
     |  __hash__ = None
    
    Help on built-in function sum in module builtins:
    
    sum(iterable, start=0, /)
        Return the sum of a 'start' value (default: 0) plus an iterable of numbers
        
        When the iterable is empty, return the start value.
        This function is intended specifically for use with numeric values and may
        reject non-numeric types.
    
    Help on built-in function min in module builtins:
    
    min(...)
        min(iterable, *[, default=obj, key=func]) -> value
        min(arg1, arg2, *args, *[, key=func]) -> value
        
        With a single iterable argument, return its smallest item. The
        default keyword-only argument specifies an object to return if
        the provided iterable is empty.
        With two or more arguments, return the smallest argument.
    
## Data Types Part 1

There are various data types, a few common examples are:

1. `int` : integer
2. `float` : floating point (decimal number)
3. `str` : string (text)
4. `bool` : boolean (i.e. True/False)

For example:


```python
myInteger = 2
myFloat = 3.1415
myString = 'apple'
myBoolean = True
```

We can also check the `type` of variables:


```python
print(type(myInteger))
print(type(myFloat))
print(type(myString))
print(type(myBoolean))
```

    <class 'int'>
    <class 'float'>
    <class 'str'>
    <class 'float'>


Another useful feature is _type casting_


```python
print(float(myInteger))
print(int(myFloat))
print(bool())
```

    2.0
    3
    False


### Exercise
1. Does int() correctly round floats?
1. What are the numerical equivalents of booleans?
1. What strings can you successfully cast into ints, floats, and booleans?

**Solution:**


```python
# Number 1
print(int(3.1415))
print(int(2.99))

# Number 2
print(float(True))
print(float(False))

# Number 3
print(float('5'))
print(float('inf'))
print(bool(6))

```

    3
    2
    1.0
    0.0
    5.0
    inf
    True


### Note on Naming Schemes

1. May consist of letters, numbers, and underscores
1. Cannot start with a number
1. Is case sensitive

For example, the following line returns an error, why?


```python
5_five = 5
print(five_5)
```

    SyntaxError: invalid token


It is also a good idea to chose variable names that are useful, for example, `blah = 3.14`, isn't particularly useful. Perhaps `pi = 3.14` is a better choice.

## Basic Math

Python is a very valuable tool for evaluating mathematical expressions. Here are some basic mathmatical operations you can peform in Python.


```python
a = 2
b = 4.5
c = "apple"

print(a+b)
print(a-b)
print(a*b)
print(a/b)
print(c+str(a))
```

    6.5
    -2.5
    9.0
    0.4444444444444444
    apple2


### Exercise
1. What do the following operators do?
    - `**`
    - `//`
    - `%`
2. What combinations of data types work and don't work?
3. Did you find anything you didn't expect?

**Solution:**


```python
# Number 1
print(3**3)
print(10//3)
print(10%3)

# Number 2
print(3**"apple")

# Number 3
print(5*"apple")
```

    27
    3
    1
    
    TypeError: unsupported operand type(s) for ** or pow(): 'int' and 'str'

    'appleappleappleappleapple'

## Conditionals

### Conditionals with Math


```python
print(3 == 3)
print(3 > 5)
print(3 < 5)
print(1 <= 2)
print(2 >= 1)
print(2 != 1)
```

    True
    False
    True
    True
    True
    True



```python
a = 5/3
b = 1 + 2/3
print(a == b)
print(a)
print(b)
```

    False
    1.6666666666666667
    1.6666666666666665



```python
print("apple" == "banana")
print(len("apple") == 5)
print("b" in "banana")
print("q" in "apple")
```

    False
    True
    True
    False


## Functions


```python
def my_first_function():
    print('I made my first function!')
    
my_first_function()
```

    I made my first function!


We can also introduce parameters into our functions.


```python
def newton_force(mass, accel=9.81):
    return mass * accel

force = newton_force(mass=100)

print(force, '[N]')

force2 = newton_force(accel=100, mass=100)

print(force2, '[N]')
```

    981.0 [N]
    10000 [N]


### Exercise
Create a function which returns the hypotenuse of a right triangle. Recall: $$c^2 = a^2 + b^2 \Rightarrow c = \sqrt{a^2 + b^2} \equiv (a^2 + b^2)^{0.5}$$

**Solution:**


```python
def hypot(a, b):
    """Put Your Code Here"""
    return (a**2 + b**2)**0.5
```


```python
hypot(3, 4)
```

    5.0


## Flow Control

### If Statements


```python
def do_it(a, b):
    if a == b:
        print("Yes")
    elif b > a:
        print("No")
    elif b < a:
        print("This other thing!")
    else:
        print("I give up")

do_it(3, 3)
do_it(10, 100)
do_it(0.1, 0)
```

    Yes
    No
    This other thing!


### While Loops


```python
a = 5
b = 1

while a > b:
    print('{} is greater than {}'.format(a,b))
    print(f"{a} is greater than {b}")
    b = b+1
    # b += 1
```

    5 is greater than 1
    5 is greater than 1
    5 is greater than 2
    5 is greater than 2
    5 is greater than 3
    5 is greater than 3
    5 is greater than 4
    5 is greater than 4


## Data Types Part 2 - Electric Boogaloo

### Lists


```python
my_list = [
    "apple", 
    "banana", 
    "shark", 
    15
]
print(my_list)
```

    ['apple', 'banana', 'shark', 15]


### Adding and Removing Elements


```python
my_list.append("ballistic missile")
print(my_list)
```

    ['apple', 'banana', 'shark', 15, 'ballistic missile']



```python
my_list.remove("banana")
print(my_list)
```

    ['apple', 'shark', 15, 'ballistic missile']


### List Indexing and Slicing


```python
print(my_list[0])
print(my_list[3])
print(my_list[1:3])
print(my_list[-1])
```

    apple
    ballistic missile
    ['shark', 15]
    shark


### Exercise

Create a function which takes a list as a parameter and an integer, n. Return the n-th entry of the list.

**Solution:**


```python
def nth_entry(a_list, n):
    """Your Code Here"""
    return a_list[n]
    
nth_entry(my_list, -1)
```




    15



### Multi-Dimensional Arrays


```python
array_2d = [[0,1,2,3], [2,5,3,2], [6,3,1,7]]
print(array_2d)
```

    [[0, 1, 2, 3], [2, 5, 3, 2], [6, 3, 1, 7]]



```python
print(array_2d[0])
print(array_2d[1][0:2])
print(array_2d[0:2])
print(array_2d[-1][-1])
```

    [0, 1, 2, 3]
    [2, 5]
    [[0, 1, 2, 3], [2, 5, 3, 2]]
    7

## Flow Control Part 2 - Back 2 Tha Hood


```python
for item in my_list:
    print(item)
```

    apple
    banana
    shark
    15



```python
my_list_2 = [1,2,3,4,5,6]

for item in my_list_2:
    print(item**2 + 3.8*item + 5.1)
```

    9.899999999999999
    16.7
    25.5
    36.3
    49.1
    63.9



```python
for item in my_list_2:
    if item > 3:
        print(item, "True")
    else:
        print(item, "False")
```

    1 False
    2 False
    3 False
    4 True
    5 True
    6 True


**`range()`** function


```python
my_range = range(len(myList))
for i in my_range:
    print('{}: {}'.format(i, myList[i]))
```

    0: apple
    1: banana
    2: shark
    3: 15


**List Comprehension**


```python
my_list_3 = [i**2 for i in my_list_2]
print(my_list_3)
```

    [1, 4, 9, 16, 25, 36]


### Exercise
Define a function that uses a for loop to draw the following pattern (out to the n-th line with n asterisks). <br>
\* <br>
\*\* <br>
\*\*\* <br>
\*\*\*\* <br>
\*\*\*\*\* <br>
...

**Solution:**


```python
list(range(5))
```




    [0, 1, 2, 3, 4]




```python
def star_tree(n):
    """Your Code Here"""
    for i in range(n):
        print('*'*(i+1))
```


```python
star_tree(n=5)
```

    *
    **
    ***
    ****
    *****


### Exercise

**Classic Challenge** : Fizz Buzz

Given a list of integers from 1 to 50. 
- Print "Fizz" if the integer is divisible by 3.
    - i.e. 3, 6, 9
- Print "Buzz" if the integer is divisible by 5. 
    - i.e. 5, 10, 15
- Print "FizzBuzz" if the integer is divisible by 3 AND 5.
    - i.e. 15, 30,  45
    
Challenge: Do it in as few lines as possible!

**Solution:**


```python
for num in range(1, 50): 
    print(num, "Fizz"*(num%3 == 0) + "Buzz"*(num%5 == 0))
```
