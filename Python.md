# Python

Python is an easy to learn, powerful programming language. It has efficient high-level data structures and a simple but effective approach to object-oriented programming.

## Whetting Your Appetite

Python can save you consideration time.

- It is an interpreted language so that you don't have to do compilation and linking;
- The usual write/compile/test/re-compile cycle is too slow. 

Python enables programs to be written compactly and readably. Programs written in Python are typically much shorter than equivalent C, C++, or Java programs, for several reasons:

- the high-level data types allow you to express complex operations in a single statement;
- statement grouping is done by indentation instead of beginning and ending brackets;
- no variable or argument declarations are necessary.

Python is *extensible*: if you know how to program in C it is easy to add a new built-in function or module to the interpreter, either to perform critical operations at maximum speed, or to link Python programs to libraries that may only be available in binary form.



## Using the Python Interpreter

On Unix/Linux system, start it by typing the command:

```shell
python3
```

Typing an end-of-file character (Control-D on Unix, Control-Z on Windows) at the primary prompt causes the interpreter to exit with a zero exit status. If that doesn’t work, you can exit the interpreter by typing the following command: `quit()` or `exit()`.

A second way of starting the interpreter is to executes the statement(s) in *command*, analogous to the shell’s `-c`option. 

```shell
python -c command [arg] ...
```

Some Python modules are also useful as scripts. Python can execute the source file for *module* as if you had spelled out its full name on the command line.

```shell
python -m module [arg] ...
```

When known to the interpreter, the script name and additional arguments thereafter are turned into a list of strings and assigned to the `argv` variable in the `sys` module. You can access this list by executing `import sys`.  Usually, `sys.argv[0]` is the name of the script. When no script and no arguments are given, `sys.argv[0]` is an empty string. When the script name is given as `'-'` (meaning standard input), `sys.argv[0]` is set to `'-'`. When [`-c`](https://docs.python.org/3/using/cmdline.html#cmdoption-c) *command* is used, `sys.argv[0]` is set to `'-c'`. When [`-m`](https://docs.python.org/3/using/cmdline.html#cmdoption-m) *module* is used, `sys.argv[0]` is set to the full name of the located module.

By default, Python source files are treated as encoded in UTF-8. To declare an encoding other than the default one, a special comment line should be added as the *first* line of the file. The syntax is as follows:

```
# -*- coding: UTF-8 -*-
```



## An Informal Introduction to Python

### Numbers

The interpreter acts as a simple calculator. In interactive mode, Python will print the value of the input expression. It supports most numerical operations.

```shell
# the simple operation of number
>>> 2 + 2, 50 - 5*6, (50 - 5*6) / 4
(4, 20, 5.0)
# division, floor division, and module
>>> 17 / 3, 17 // 3, 17 % 3
(5.6666666666666667, 5, 2)
# power
>> 2 ** 7
128
 # '_' represents the value of last expression
>>> _ - 2
126
```

### Strings

Python can also manipulate strings, which is enclosed in quotes.

````shell
# single quotes and double quotes are the same
>>> 'hello', "world'
('hello', 'world')
# esacpe and the print()
>>> 'Mary said "I don\'t like it."'
'Mary said "I don\'t like it."'
>>> print('Mary said "I don\'t like it."')
Mary said "I don't like it."
# using 'r' to prevent escape
>>> r'C:\user'
'C:\\user'
# multiple lines string, using '\' at the end of line to prevent add new line
>>> print("""\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
""")
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
# concatenate string with the + operator, and repeated with *
>>> 3 * 'un' + 'ium'
'unununium'
# string literals next to each other are automatically concatenated.
>>> 'Py' 'thon'
'Python'
# character during string can be get using index
>>> word = 'Python'
>>> word[0]  # character in position 0
'P'
# index can be negative numbers
>>> word[-1]  # last character
'n'
# index out of length will raise an exception
>>> word[42]  # the word only has 6 characters
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
# use index to get substring
>>> word[1:2], word[:2], word[4:], word[-3:]
('y', 'Py', 'on', 'hon')
# strings are immutable, which means they cannot be changed
>>> word[0] = 'J'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
# create a new one if you need a different string
>>> 'J' + word[1:]
'Jython'
# len() returns the length of a string
>>> len('supercalifragilisticexpialidocious')
34
````

### Lists

Python knows a number of *compound* data types, used to group together other values. The most versatile is the *list*, which can be written as a list of comma-separated values (items) between square brackets. 

```shell
# list can contain items of different types
>>> ['hello', 2019]
['hello', 2019]
# lists can be indexed and sliced
>>> squares = [1, 4, 9, 16, 25]
>>> squares[0], squares[-1], squares[-3:]
(1, 25, [9, 16, 25])
# slices always return a new list, list[:] means a new copy
>>> cubes = squares[:]
[1, 4, 9, 16, 25]
# lists also support operations like concatenation
>>> squares + [36, 49, 64, 81, 100]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
# lists are a mutable type
>>> cubes.append(216)
>>> cubes[6] = 36
# assignment to slices is also possible
>>> letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> letters[2:5] = ['C', 'D', 'E']
>>> letters
 ['a', 'b', 'C', 'D', 'E', 'f', 'g']
>>> letters[:] = []
>>> letters
[]
# len() also applies to lists
>>> len(letters)
0
# it is possible to nest lists
>>> a = ['a', 'b', 'c']
>>> n = [1, 2, 3]
>>> x = [a, n]
>>> x
[['a', 'b', 'c'], [1, 2, 3]]
```



## More Control Flow Tools

### `if` Statements

```python
if x < 0:
    x = 0
    print('Negative changed to zero')
elif x == 0:
    print('Zero')
elif x == 1:
    print('Single')
else:
    print('More')
```

If statement can be shorten into one line when its body is simple:

```python
x = 0 if x < 0 else x
```

### `for` Statements

Rather than always iterating over an arithmetic progression of numbers (like in Pascal), or giving the user the ability to define both the iteration step and halting condition (as C), Python’s `for` statement iterates over the items of any sequence (a list or a string).

```python
for w in words:
    print(w, len(w))
```

If you need to modify the sequence you are iterating over while inside the loop (for example to duplicate selected items), it is recommended that you first make a copy. The slice notation makes this especially convenient.

```python
for w in words[:]:  # Loop over a slice copy of the entire list.
    if len(w) > 6:
        words.insert(0, w)
```

### The `range()` Function

If you do need to iterate over a sequence of numbers, the built-in function [`range()`](https://docs.python.org/3/library/stdtypes.html#range) comes in handy. It generates arithmetic progressions:

```python
for i in range(5): # 0 1 2 3 4 
    print(i)
```

The given end point is never part of the generated sequence. It is possible to let the range start at another number, or to specify a different increment.

```python
range(5, 10) 			# 5, 6, 7, 8, 9
range(0, 10, 3)			# 0, 3, 6, 9
range(-10, -100, -30)	# -10, -40, -70
```

To iterate over the indices of a sequence, you can combine `range()` and `len()` as follows:

```python
for i in range(len(a)):
    print(i, a[i])
```

In many ways the object returned by `range()`behaves as if it is a list, but in fact it isn't. It is an object which returns the successive items of the desired sequence when you iterate over it, but it doesn't really make the list, thus saving space.

### `break` and `continue` Statements, and `else` Clauses on Loops

The `break` statement breaks out of the innermost enclosing `for` or `while` loop. The `continue` statement continues with the next iteration of the loop:

Loop statements may have an `else` clause; it is executed when the loop terminates through exhaustion of the list (with `for`) or when the condition becomes false (with `while`), but not when the loop is terminated by a `break` statement.

```python
>>> for n in range(1, 10):
...     if n == 1:
...          continue;
...     for x in range(2, n):
...         if n % x == 0:
...             print(n, 'equals', x, '*', n//x)
...             break
...     else:
...         # loop fell through without finding a factor
...         print(n, 'is a prime number')
...
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```

### `pass` Statements

The `pass` statement does nothing. It can be used when a statement is required syntactically but the program requires no action. 

```python
while True:
    pass  # Busy-wait for keyboard interrupt (Ctrl+C)
class MyEmptyClass:
    pass  # Creating minimal classes
def initlog(*args):
    pass   # Remember to implement this!
```

### Defining Functions

The keyword `def` introduces a function *definition*. The statements that form the body of the function start at the next line, and must be indented.

```python
>>> def fib(n):    # write Fibonacci series up to n
...     """Print a Fibonacci series up to n."""
...     a, b = 0, 1
...     while a < n:
...         print(a, end=' ')
...         a, b = b, a+b
...     print()
...
>>> # Now call the function we just defined:
... fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
```

#### Symbol table

The *execution* of a function introduces a new symbol table used for the local variables of the function. More precisely, all variable assignments in a function store the value in the local symbol table; whereas variable references first look in the **local symbol table**, then in the local **symbol tables of enclosing functions**, then in the **global symbol table**, and finally in the **table of built-in names**. This is called **'LEGB'** protocol.

#### Function arguments

The actual parameters (arguments) to a function call are introduced in the local symbol table of the called function when it is called; thus, arguments are passed using *call by value* (where the ***value*** is always **an object *reference***, not the value of the object). When a function calls another function, a new local symbol table is created for that call.

#### Function object

A function definition introduces the function name in the current symbol table. The value of the function name has a type that is recognized by the interpreter as a user-defined function. This value can be assigned to another name which can then also be used as a function. 

```python
>>> fib
<function fib at 10042ed0>
>>> f = fib
>>> f(100)
0 1 1 2 3 5 8 13 21 34 55 89
```

#### Function return

Function can return a value. If no value is returned, function return `None`.

#### Default Argument Values

The most useful form is to specify a default value for one or more arguments. 

```python
def ask_ok(prompt, retries=4, reminder='Please try again!'):
    pass
```

The default values are evaluated at the point of function definition in the *defining* scope.

```python
>>> i = 5
>>> def f(arg=i):
...     print(arg)
>>> i = 6
>>> f()
5
```

The default value is evaluated only once. This makes a difference when the default is a mutable object such as a list, dictionary, or instances of most classes.

```python
>>> def f(a, L=[]):
...     L.append(a)
...     return L
>>> print(f(1))
[1]
>>> print(f(2))
[1, 2]
>>> print(f(3))
[1, 2, 3]
```

#### Keyword Arguments

Functions can also be called using keyword arguments of the form `kwarg=value`.

```python
def parrot(voltage, state='a stiff', action='voom', type='Norwegian Blue'):
	pass
# These are ok
parrot(1000)                                          # 1 positional argument
parrot(voltage=1000)                                  # 1 keyword argument
parrot(voltage=1000000, action='VOOOOOM')             # 2 keyword arguments
parrot(action='VOOOOOM', voltage=1000000)             # 2 keyword arguments
parrot('a million', 'bereft of life', 'jump')         # 3 positional arguments
parrot('a thousand', state='pushing up the daisies')  # 1 positional, 1 keyword
# These are invalid
parrot()                     	# required argument missing
parrot(voltage=5.0, 'dead')  	# non-keyword argument after a keyword argument
parrot(110, voltage=220)     	# duplicate value for the same argument
parrot(actor='John Cleese')  	# unknown keyword argument
```

#### Arbitrary Argument Lists

These arguments will be wrapped up in a tuple. 

```python
def write_multiple_items(file, separator, *args):
    file.write(separator.join(args))
```

Normally, these `variadic` arguments will be last in the list of formal parameters, because they scoop up all remaining input arguments that are passed to the function. Any formal parameters which occur after the `*args`parameter are ‘keyword-only’ arguments, meaning that they can only be used as keywords rather than positional arguments.

```python
def concat(*args, sep="/"):
    return sep.join(args)
```

#### Unpacking Argument Lists

The reverse situation occurs when the arguments are already in a list or tuple but need to be unpacked for a function call requiring separate positional arguments. If they are not available separately, write the function call with the `*` operator to unpack the arguments out of a list or tuple.

```python
>>> args = [3, 6]
>>> list(range(*args))            # call with arguments unpacked from a list
[3, 4, 5]
```

In the same fashion, dictionaries can deliver keyword arguments with the `**` operator:

```python
>>> def parrot(voltage, state='a stiff', action='voom'):
...     print("-- This parrot wouldn't", action, end=' ')
...     print("if you put", voltage, "volts through it.", end=' ')
...     print("E's", state, "!")
>>> d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
>>> parrot(**d)
-- This parrot wouldn't VOOM if you put four million volts through it. E's bleedin' demised !
```

Another example:

```python
>>> def cheeseshop(kind, *arguments, **keywords): # *name must occur before **name
...     print("-- Do you have any", kind, "?")
...     print("-- I'm sorry, we're all out of", kind)
...     for arg in arguments:
...         print(arg)
...     print("-" * 40)
...     for kw in keywords:
...         print(kw, ":", keywords[kw])
...
>>> cheeseshop("Limburger", "It's very runny, sir.",
...            "It's really very, VERY runny, sir.",
...            shopkeeper="Michael Palin",
...            client="John Cleese",
...            sketch="Cheese Shop Sketch")
...
-- Do you have any Limburger ?
-- I'm sorry, we're all out of Limburger
It's very runny, sir.
It's really very, VERY runny, sir.
----------------------------------------
shopkeeper : Michael Palin
client : John Cleese
sketch : Cheese Shop Sketch
```

#### Lambda Expressions

Small anonymous functions can be created with the `lambda` keyword. 

```python
>>> def make_incrementor(n):
...     return lambda x: x + n
...
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43
```

#### Documentation Strings

The first statement of the function body can optionally be a string literal; this string literal is the function’s documentation string, or *docstring*.

There are tools which use docstrings to automatically produce online or printed documentation, or to let the user interactively browse through code; it’s good practice to include docstrings in code that you write, so make a habit of it.

The first line should always be a short, concise summary of the object’s purpose. This line should begin with a capital letter and end with a period. If there are more lines in the documentation string, the second line should be blank, visually separating the summary from the rest of the description. The following lines should be one or more paragraphs describing the object’s calling conventions, its side effects, etc.

```python
>>> def my_function():
...     """Do nothing, but document it.
...
...     No, really, it doesn't do anything.
...     """
...     pass
...
>>> print(my_function.__doc__)
Do nothing, but document it.

    No, really, it doesn't do anything.
```

####  Function Annotations

Function annotations are completely optional metadata information about the types used by user-defined functions. 

```python
>>> def f(ham: str, eggs: str = 'eggs') -> str:
...     print("Annotations:", f.__annotations__)
...     print("Arguments:", ham, eggs)
...     return ham + ' and ' + eggs
...
>>> f('spam')
Annotations: {'ham': <class 'str'>, 'return': <class 'str'>, 'eggs': <class 'str'>}
Arguments: spam eggs
'spam and eggs'
```



## Data Structures

### More on Lists

An example that uses most of the list methods

```python
# initialization
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
# count the number of an item
>>> fruits.count('apple'), fruits.count('tangerine')
(2,0)
# get the index of an item
>>> fruits.index('banana'), fruits.index('banana', 4)  # Find banana starting at 4
(3, 6)
# reverse the order of items
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
# add an item
>>> fruits.append('grape')
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange', 'grape']
# sort the items
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'grape', 'kiwi', 'orange', 'pear']
# pop the last item
>>> fruits.pop()
'pear'
```

#### Using Lists as stack or queue

The list methods make it very easy to use a list as a stack, , where the last element added is the first element retrieved (“last-in, first-out”). 

```python
>>> stack = [3, 4, 5]
>>> stack.append(7) 	# add an item
>>> stack.pop()			# remove the latest item
```

The lists are not efficient to use as queue. To implement a queue, use `collections.deque` which was designed to have fast appends and pops from both ends.

```python
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # add an item
>>> queue.popleft()                 # remove the oldest item
```

####  List Comprehensions

List comprehensions provide a concise way to create lists.

```python
>>> squares = [x**2 for x in range(10)]
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> # which is same with
squares = []
>>> for x in range(10):
...     squares.append(x**2)
```

A list comprehension consists of brackets containing an expression followed by a `for` clause, then zero or more `for` or `if` clauses. 

```python
>>> [(x, y) for x in [1,2,3] for y in [3,1,4] if x != y]
[(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
>>> # which is same with
>>> combs = []
>>> for x in [1,2,3]:
...     for y in [3,1,4]:
...         if x != y:
...             combs.append((x, y))
```

Some more examples:

```python
>>> vec = [-4, -2, 0, 2, 4]
>>> # create a new list with the values doubled
>>> [x*2 for x in vec]
[-8, -4, 0, 4, 8]
>>> # filter the list to exclude negative numbers
>>> [x for x in vec if x >= 0]
[0, 2, 4]
>>> # apply a function to all the elements
>>> [abs(x) for x in vec]
[4, 2, 0, 2, 4]
>>> # call a method on each element
>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
>>> [weapon.strip() for weapon in freshfruit]
['banana', 'loganberry', 'passion fruit']
>>> # create a list of 2-tuples like (number, square)
>>> [(x, x**2) for x in range(6)]
[(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
>>> # the tuple must be parenthesized, otherwise an error is raised
>>> [x, x**2 for x in range(6)]
  File "<stdin>", line 1, in <module>
    [x, x**2 for x in range(6)]
               ^
SyntaxError: invalid syntax
>>> # flatten a list using a listcomp with two 'for'
>>> vec = [[1,2,3], [4,5,6], [7,8,9]]
>>> [num for elem in vec for num in elem]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Nested List Comprehensions is valid.

```python
>>> matrix = [
...     [1, 2, 3, 4],
...     [5, 6, 7, 8],
...     [9, 10, 11, 12],
... ]
>>> [[row[i] for row in matrix] for i in range(4)]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
>>> # which is same with
>>> transposed = []
>>> for i in range(4):
...     # the following 3 lines implement the nested listcomp
...     transposed_row = []
...     for row in matrix:
...         transposed_row.append(row[i])
...     transposed.append(transposed_row)
```

### The `del` statement

There is a way to remove an item from a list given its index instead of its value.

```python
>>> a = [-1, 1, 66.25, 333, 333, 1234.5]
>>> del a[0]
>>> a
[1, 66.25, 333, 333, 1234.5]
>>> del a[2:4]
>>> a
[1, 66.25, 1234.5]
>>> del a[:]
>>> a
[]
>> del a
>>> a
Traceback (most recent call last):
	File "<stdin>", line 1, in <module>
NameError: name 'a' is not defined
```

### Tuples and Sequences

Python support other sequence data types. Tuples are similar with list, enclosed in parentheses.  In different cases, parentheses can be omitted. While on output tuples are always enclosed in parentheses, they may be input with or without surrounding parentheses.

```python
>>> t = 12345, 54321, 'hello!'			# input tuple
>>> t
(12345, 54321, 'hello!')				# output tuple
```

It is not possible to assign to the individual items of a tuple, however it is possible to create tuples which contain mutable objects, such as lists.

```python
>>> # Tuples are immutable:
... t[0] = 88888
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> # but they can contain mutable objects:
... v = ([1, 2, 3], [3, 2, 1])
>>> v
([1, 2, 3], [3, 2, 1])
```

Though tuples may seem similar to lists, they are often used in different situations and for different purposes. Tuples are immutable, and usually contain a heterogeneous sequence of elements that are accessed via unpacking (see later in this section) or indexing (or even by attribute in the case of `namedtuples`). Lists are mutable, and their elements are usually homogeneous and are accessed by iterating over the list.

A special problem is the construction of tuples containing 0 or 1 items.

```python
>>> empty = ()					# empty tuple
>>> singleton = 'hello',		# prefer ('hello')
```

*tuple packing* is used everywhere. For example, multiple assignment is really just a combination of tuple packing and sequence unpacking.

```python
>>> t = 12345, 54321, 'hello!'
>>> x, y, z = t
```

###  Sets

A set is an unordered collection with no duplicate elements. Basic uses include membership testing and eliminating duplicate entries.

```python
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)                      # show that duplicates have been removed
{'orange', 'banana', 'pear', 'apple'}
>>> 'orange' in basket                 # fast membership testing
True
>>> 'crabgrass' in basket
False
```

Set objects also support mathematical operations like union, intersection, difference, and symmetric difference.

```python
>>> # Demonstrate set operations on unique letters from two words
...
>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
{'a', 'r', 'b', 'c', 'd'}
>>> a - b                              # letters in a but not in b
{'r', 'd', 'b'}
>>> a | b                              # letters in a or b or both
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
>>> a & b                              # letters in both a and b
{'a', 'c'}
>>> a ^ b                              # letters in a or b but not both
{'r', 'd', 'b', 'm', 'z', 'l'}
```

Similarly to list comprehensions, set comprehensions are also supported:

```python
>>> a = {x for x in 'abracadabra' if x not in 'abc'}
>>> a
{'r', 'd'}
```

### Dictionaries

Dictionaries are sometimes found in other languages as “associative memories” or “associative arrays”. Unlike sequences, which are indexed by a range of numbers, dictionaries are indexed by *keys*, which can be any immutable type; strings and numbers can always be keys. Tuples can be used as keys if they contain only strings, numbers, or tuples; if a tuple contains any mutable object either directly or indirectly, it cannot be used as a key.

It is best to think of a dictionary as a set of *key: value* pairs, with the requirement that the keys are unique (within one dictionary).

```python
>>> tel = {'jack': 4098, 'sape': 4139}
>>> tel['guido'] = 4127
>>> tel
{'jack': 4098, 'sape': 4139, 'guido': 4127}
>>> tel['jack']
4098
>>> del tel['sape']
>>> tel['irv'] = 4127
>>> tel
{'jack': 4098, 'guido': 4127, 'irv': 4127}
>>> list(tel)
['jack', 'guido', 'irv']
>>> sorted(tel)
['guido', 'irv', 'jack']
>>> 'guido' in tel
True
>>> 'jack' not in tel
False
```

The `dict()` constructor builds dictionaries directly from sequences of key-value pairs:

```python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```

In addition, dict comprehensions can be used to create dictionaries from arbitrary key and value expressions:

```python
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
```

When the keys are simple strings, it is sometimes easier to specify pairs using keyword arguments:

```python
>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'guido': 4127, 'jack': 4098}
```

### Looping Techniques

When looping through dictionaries, the key and corresponding value can be retrieved at the same time using the `items()` method.

```python
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
```

When looping through a sequence, the position index and corresponding value can be retrieved at the same time using the `enumerate()` function.

```python
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)
```

To loop over two or more sequences at the same time, the entries can be paired with the `zip()` function.

```python
>>> questions = ['name', 'quest', 'favorite color']
>>> answers = ['lancelot', 'the holy grail', 'blue']
>>> for q, a in zip(questions, answers):
...     print('What is your {0}?  It is {1}.'.format(q, a))
```

### More on Conditions

The comparison operators `in` and `not in` check whether a value occurs (does not occur) in a sequence. The operators `is` and `is not` compare whether two objects are really the same object; this only matters for mutable objects like lists.

Comparisons can be chained. For example, `a < b == c` tests whether `a` is less than `b` and moreover `b` equals `c`.

Comparisons may be combined using the Boolean operators `and` and `or`, and the outcome of a comparison (or of any other Boolean expression) may be negated with `not`.

The Boolean operators `and` and `or` are so-called *short-circuit* operators: their arguments are evaluated from left to right, and evaluation stops as soon as the outcome is determined.



## Scope and Namespace

### A Word About Names and Objects

Objects have individuality, and multiple names (in multiple scopes) can be bound to the same object. This is known as aliasing in other languages.

This is usually not appreciated on a first glance at Python, and can be safely ignored when dealing with immutable basic types (numbers, strings, tuples). However, aliasing has a possibly surprising effect on the semantics of Python code involving mutable objects such as lists, dictionaries, and most other types.

This is usually used to the benefit of the program, since aliases behave like pointers in some respects. For example, passing an object is cheap since only a pointer is passed by the implementation; and if a function modifies an object passed as an argument, the caller will see the change.

### Python Scopes and Namespaces

A *namespace* is a mapping from names to objects. Most namespaces are currently implemented as Python dictionaries, but that’s normally not noticeable in any way (except for performance), and it may change in the future. 

Examples of namespaces are: the set of built-in names (containing functions such as `abs()`, and built-in exception names); the global names in a module; and the local names in a function invocation.

Namespaces are created at different moments and have different lifetimes. The namespace containing the built-in names is created when the Python interpreter starts up, and is never deleted. The global namespace for a module is created when the module definition is read in; normally, module namespaces also last until the interpreter quits. The local namespace for a function is created when the function is called, and deleted when the function returns or raises an exception that is not handled within the function. 

A *scope* is a textual region of a Python program where a namespace is directly accessible. “Directly accessible” here means that an unqualified reference to a name attempts to find the name in the namespace.

At any time during execution, there are at least three nested scopes whose namespaces are directly accessible:

- **L**, the innermost scope, which is searched first, contains the local names
- **E**, the scopes of any enclosing functions, which are searched starting with the nearest enclosing scope, contains non-local, but also non-global names
- **G**, the next-to-last scope contains the current module’s global names
- **B**, the outermost scope (searched last) is the namespace containing built-in names

The `global` statement can be used to indicate that particular variables live in the global scope and should be rebound there; the `nonlocal ` statement indicates that particular variables live in an enclosing scope and should be rebound there.

```python
>>> def scope_test():
...     def do_local():
...         spam = "local spam"
... 
...     def do_nonlocal():
...         nonlocal spam
...         spam = "nonlocal spam"
... 
...     def do_global():
...         global spam
...         spam = "global spam"
... 
...     spam = "test spam"
...     do_local()
...     print("After local assignment:", spam)
...     do_nonlocal()
...     print("After nonlocal assignment:", spam)
...     do_global()
...     print("After global assignment:", spam)
... 
>>> scope_test()
After local assignment: test spam
After nonlocal assignment: nonlocal spam
After global assignment: nonlocal spam
>>> print("In global scope:", spam)
In global scope: global spam
```



## Classes

Classes provide a means of bundling data and functionality together. Creating a new class creates a new *type* of object, allowing new *instances* of that type to be made. Each class instance can have attributes attached to it for maintaining its state. Class instances can also have methods (defined by its class) for modifying its state.

Compared with other programming languages, Python’s class mechanism adds classes with a minimum of new syntax and semantics.

- Normally class members (including the data members) are *public*.
- All member functions are *virtual*.
- The method function is declared with an explicit first argument representing the object, which is provided implicitly by the call.
- The class inheritance mechanism allows multiple base classes.  
- A derived class can override any methods of its base class or classes.
- A method can call the method of a base class with the same name.
- Built-in types can be used as base classes for extension by the user.
- Most built-in operators with special syntax (arithmetic operators, subscripting etc.) can be redefined for class instances.
- Classes themselves are objects. This provides semantics for importing and renaming.

### A First Glance at Classes

The simplest form of class definition looks like this:

```python
class ClassName:
    <statement-1>
    .
    <statement-N>
```

Class definitions, like function definitions ([`def`](https://docs.python.org/3/reference/compound_stmts.html#def) statements) must be executed before they have any effect.

When a class definition is entered, a new namespace is created, and used as the local scope — thus, all assignments to local variables go into this new namespace. In particular, function definitions bind the name of the new function here.

#### Class Objects

Class objects support two kinds of operations: attribute references and instantiation. If a class definition looked like this:

```python
class MyClass:
    """A simple example class"""
    i = 12345

    def f(self):
        return 'hello world'
```

*Attribute references* use the standard syntax used for all attribute references in Python: `obj.name`.  In class MyClass, `MyClass.i` and `MyClass.f` are valid attribute references, returning an integer and a function object, respectively. `__doc__` is also a valid attribute, returning the docstring belonging to the class: `"A simple example class"`.

Class *instantiation* uses function notation. Just pretend that the class object is a parameterless function that returns a new instance of the class.

```python
x = MyClass()
```

 Many classes like to create objects with instances customized to a specific initial state. When a class defines an `__init__()` method, class instantiation automatically invokes `__init__()` for the newly-created class instance. the `__init__()` method may have arguments for greater flexibility. In that case, arguments given to the class instantiation operator are passed on to `__init__()`.

```python
>>> class Complex:
...     def __init__(self, realpart, imagpart):
...         self.r = realpart
...         self.i = imagpart
...
>>> x = Complex(3.0, -4.5)
>>> x.r, x.i
(3.0, -4.5)
```

#### Instance Objects

The only operations understood by instance objects are attribute references. There are two kinds of valid attribute names, data attributes and methods.

Data attributes need not be declared; like local variables, they spring into existence when they are first assigned to.

```python
x.counter = 1                     # declare a data attribute 'x'
while x.counter < 10:
    x.counter = x.counter * 2
print(x.counter)
del x.counter					  # delete 'x'
```

 A method is a function that “belongs to” an object. Valid method names of an instance object depend on its class. By definition, all attributes of a class that are function objects define corresponding methods of its instances. 

So in our example, `x.f` is a valid method reference, since `MyClass.f` is a function, but `x.i` is not, since `MyClass.i` is not. But `x.f` is not the same thing as `MyClass.f` — it is a *method object*, not a function object.

Usually, a method is called right after it is bound, but it is ok to store the method object to call it later.

```python
x.f()			# call right away
xf = x.f()
xf()			# call later
```

The special thing about methods is that the instance object is passed as the first argument of the function. In general, calling a method with a list of *n* arguments is equivalent to calling the corresponding function with an argument list that is created by inserting the method’s instance object before the first argument.

```python
MyClass.f(x)	# equivalent to x.f()
```

#### Class and Instance Variables

Generally speaking, instance variables are for data unique to each instance and class variables are for attributes and methods shared by all instances of the class. Shared data can have possibly surprising effects with involving [mutable](https://docs.python.org/3/glossary.html#term-mutable) objects such as lists and dictionaries.

```python
class Dog:

    kind = 'canine'         # class variable shared by all instances
    tricks = []             # mistaken use of a class variable

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.kind                  # shared by all dogs
'canine'
>>> e.kind                  # shared by all dogs
'canine'
>>> d.name                  # unique to d
'Fido'
>>> e.name                  # unique to e
'Buddy'
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks                # unexpectedly shared by all dogs
['roll over', 'play dead']
```

####  Something about method

Data attributes override method attributes with the same name; to avoid accidental name conflicts, which may cause hard-to-find bugs in large programs, it is wise to use some kind of convention that minimizes the chance of conflicts.

Any function object that is a class attribute defines a method for instances of that class. It is not necessary that the function definition is textually enclosed in the class definition: assigning a function object to a local variable in the class is also ok. For example:

```python
# Function defined outside the class
def f1(self, x, y):
    return min(x, x+y)

class C:
    f = f1
```

Methods may call other methods by using method attributes of the `self` argument:

```python
class Bag:
    def __init__(self):
        self.data = []

    def add(self, x):
        self.data.append(x)

    def addtwice(self, x):
        self.add(x)
        self.add(x)
```

### A Deep look at Classes

#### Inheritance

 The syntax for a derived class definition looks like this:

```python
class DerivedClassName(BaseClassName):
    <statement-1>
    .
    <statement-N>
```

Execution of a derived class definition proceeds the same as for a base class. When the class object is constructed, the base class is remembered. This is used for resolving attribute references: if a requested attribute is not found in the class, the search proceeds to look in the base class. This rule is applied recursively if the base class itself is derived from some other class.

Derived classes may override methods of their base classes. Because methods have no special privileges when calling other methods of the same object, a method of a base class that calls another method defined in the same base class may end up calling a method of a derived class that overrides it. (For C++ programmers: all methods in Python are effectively `virtual`.)

```python
class Base:
	def foo(self):
		print('Base')
	def run(self):
		self.foo()

class Derived(Base):
	def foo(self):
		print('Derived')

>>> b = Derived()
>>> b.run()
Derived
>>> Base.foo(b)
Base
```

Python supports a form of multiple inheritance as well.

```python
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
    .
    <statement-N>
```

For most purposes, in the simplest cases, you can think of the search for attributes inherited from a parent class as depth-first, left-to-right, not searching twice in the same class where there is an overlap in the hierarchy. Thus, if an attribute is not found in `DerivedClassName`, it is searched for in `Base1`, then (recursively) in the base classes of `Base1`, and if it was not found there, it was searched for in `Base2`, and so on.

In fact, it is slightly more complex than that. The method resolution order changes dynamically. Dynamic ordering is necessary because all cases of multiple inheritance exhibit one or more diamond relationships (where at least one of the parent classes can be accessed through multiple paths from the bottommost class). For example, all classes inherit from `object`, so any case of multiple inheritance provides more than one path to reach `object`. To keep the base classes from being accessed more than once, the dynamic algorithm linearizes the search order in a way that preserves the left-to-right ordering specified in each class, that calls each parent only once, and that is monotonic (meaning that a class can be subclassed without affecting the precedence order of its parents). 

This approach is known in some other multiple-inheritance languages as *call-next-method* and is more powerful than the super call found in single-inheritance languages. 

#### Private Variables

“Private” instance variables that cannot be accessed except from inside an object don’t exist in Python.

However, there is a convention that is followed by most Python code: a name prefixed with an underscore (e.g. `_spam`) should be treated as a non-public part of the API (whether it is a function, a method or a data member). It should be considered an implementation detail and subject to change without notice.

Since there is limited support for such a mechanism, called *name mangling*. Any identifier of the form `__spam` (at least two leading underscores, at most one trailing underscore) is textually replaced with `_classname__spam`, where `classname` is the current class name with leading underscore(s) stripped. This mangling is done without regard to the syntactic position of the identifier, as long as it occurs within the definition of a class.

#### Iterators

By now you have probably noticed that most container objects can be looped over using a [`for`](https://docs.python.org/3/reference/compound_stmts.html#for) statement:

```python
for element in [1, 2, 3]:
    print(element)
```

This style of access is clear, concise, and convenient. The use of iterators pervades and unifies Python. Behind the scenes, the `for` statement calls `iter()` on the container object. The function returns an iterator object that defines the method `__next__()` which accesses elements in the container one at a time. When there are no more elements, `__next__()` raises a `StopIteration` exception which tells the `for` loop to terminate. You can call the `__next__()` method using the `next()` built-in function.

```python 
>>> s = 'abc'
>>> it = iter(s)
>>> it
<iterator object at 0x00A1DB50>
>>> next(it)
'a'
>>> next(it)
'b'
>>> next(it)
'c'
>>> next(it)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    next(it)
StopIteration
```

Having seen the mechanics behind the iterator protocol, it is easy to add iterator behavior to your classes. Define an `__iter__()` method which returns an object with a `__next__()` method. If the class defines `__next__()`, then `__iter__()`can just return `self`:

```python
class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]
    
>>> rev = Reverse('spam')
>>> iter(rev)
<__main__.Reverse object at 0x00A1DB50>
>>> for char in rev:
...     print(char)
...
m
a
p
s
```

#### Generators

Generators are a simple and powerful tool for creating iterators. They are written like regular functions but use the `yield` statement whenever they want to return data. Each time `next()` is called on it, the generator resumes where it left off (it remembers all the data values and which statement was last executed). An example shows that generators can be trivially easy to create:

```python
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]
>>> for char in reverse('golf'):
...     print(char)
...
f
l
o
g
```

Anything that can be done with generators can also be done with class-based iterators as described in the previous section. What makes generators so compact is that the `__iter__()`and `__next__()`methods are created automatically.

#### Generator Expressions

Some simple generators can be coded succinctly as expressions using a syntax similar to list comprehensions but with parentheses instead of square brackets. These expressions are designed for situations where the generator is used right away by an enclosing function. Generator expressions are more compact but less versatile than full generator definitions and tend to be more memory friendly than equivalent list comprehensions.

```python
>>> (i*i for i in range(10)						# genexpr object
<generator object <genexpr> at 0x7fce0bd50360>
>>> sum(i*i for i in range(10))                 # sum of squares
285
>>> xvec = [10, 20, 30]
>>> yvec = [7, 5, 3]
>>> sum(x*y for x,y in zip(xvec, yvec))         # dot product
260
>>> data = 'golf'
>>> list(data[i] for i in range(len(data)-1, -1, -1))
['f', 'l', 'o', 'g']
```



## Modules

Python has a way to put definitions in a file and use them in a script or in an interactive instance of the interpreter. Such a file is called a *module*; definitions from a module can be *imported* into other modules or into the *main* module. (the collection of variables that you have access to in a script executed at the top level and in calculator mode).

A module is a file containing Python definitions and statements. The file name is the module name with the suffix `.py` appended. Within a module, the module’s name (as a string) is available as the value of the global variable`__name__`.

For instance, use your favorite text editor to create a file called `fibo.py` in the current directory with the following contents:

```python
# Fibonacci numbers module

def fib(n):    # write Fibonacci series up to n
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

def fib2(n):   # return Fibonacci series up to n
    result = []
    a, b = 0, 1
    while a < n:
        result.append(a)
        a, b = b, a+b
    return result
```

Import this module and you can access the functions using the module name.

```python
>>> import fibo
>>> fibo.fib(1000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
```

### More on Modules

A module can contain executable statements as well as function definitions. These statements are intended to initialize the module. They are executed only the *first* time the module name is encountered in an import statement.

Each module has its own private symbol table, which is used as the global symbol table by all functions defined in the module. Thus, the author of a module can use global variables in the module without worrying about accidental clashes with a user’s global variables. On the other hand, if you know what you are doing you can touch a module’s global variables with the same notation used to refer to its functions, `modname.itemname`.

There are some variant of the `import` statement:

```python
from fibo import fib, fib2
from fibo import *
import fibo as fib
from fibo import fib as fibonacci
```

Note that `import *` imports all names except those beginning with an underscore (`_`). In most cases Python programmers do not use this facility since it introduces an unknown set of names into the interpreter, possibly hiding some things you have already defined.

For efficiency reasons, each module is only imported once per interpreter session. Therefore, if you change your modules, you must restart the interpreter – or, if it’s just one module you want to test interactively, use `importlib.reload()`.

```python
import importlib
importlib.reload(modulename)
```

#### Executing modules as scripts

When you run a Python module with

```python
python fibo.py <arguments>
```

the code in the module will be executed, just as if you imported it, but with the `__name__` set to `"__main__"`. That means that by adding this code at the end of your module:

```python
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```

you can make the file usable as a script as well as an importable module, because the code that parses the command line only runs if the module is executed as the “main” file.

#### The Module Search Path

When a module named `spam` is imported, the interpreter first searches for a built-in module with that name. If not found, it then searches for a file named `spam.py` in a list of directories given by the variable `sys.path`.

`sys.path` is initialized from these locations:

- The directory containing the input script (or the current directory when no file is specified).
- `PYTHONPATH`(a list of directory names, with the same syntax as the shell variable `PATH`).
- The installation-dependent default.

After initialization, Python programs can modify `sys.path`.

```python
import sys
sys.path.append('/ufs/guido/lib/python')
```

The directory containing the script being run is placed at the beginning of the search path, ahead of the standard library path. This means that scripts in that directory will be loaded instead of modules of the same name in the library directory. This is an error unless the replacement is intended. 

#### “Compiled” Python files

To speed up loading modules, Python caches the compiled version of each module in the `__pycache__` directory under the name `module.*version*.pyc`, for instance, `__pycache__/spam.cpython-33.pyc`. 

The compiled modules are platform-independent, so the same library can be shared among systems with different architectures. Python checks the modification date of the source against the compiled version to see if it’s out of date and needs to be recompiled. 

Python does not check the cache in two circumstances. First, it always recompiles and does not store the result for the module that’s loaded directly from the command line. Second, it does not check the cache if there is no source module. To support a non-source (compiled only) distribution, the compiled module must be in the source directory, and there must not be a source module.

### The `dir()` Function

The built-in function `dir()` is used to find out which names a module defines. It returns a sorted list of strings:

```python
>>> import fibo, sys
>>> dir(fibo)
['__name__', 'fib', 'fib2']
>>> dir(sys)  
['__displayhook__', '__doc__', '__excepthook__', '__loader__', '__name__',
 '__package__', '__stderr__', '__stdin__', '__stdout__',
 '_clear_type_cache', '_current_frames', '_debugmallocstats', '_getframe',
 '_home', '_mercurial', '_xoptions', 'abiflags', 'api_version', 'argv',
 'base_exec_prefix', 'base_prefix', 'builtin_module_names', 'byteorder',
 'call_tracing', 'callstats', 'copyright', 'displayhook',
 'dont_write_bytecode', 'exc_info', 'excepthook', 'exec_prefix',
 'executable', 'exit', 'flags', 'float_info', 'float_repr_style',
 'getcheckinterval', 'getdefaultencoding', 'getdlopenflags',
 'getfilesystemencoding', 'getobjects', 'getprofile', 'getrecursionlimit',
 'getrefcount', 'getsizeof', 'getswitchinterval', 'gettotalrefcount',
 'gettrace', 'hash_info', 'hexversion', 'implementation', 'int_info',
 'intern', 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path',
 'path_hooks', 'path_importer_cache', 'platform', 'prefix', 'ps1',
 'setcheckinterval', 'setdlopenflags', 'setprofile', 'setrecursionlimit',
 'setswitchinterval', 'settrace', 'stderr', 'stdin', 'stdout',
 'thread_info', 'version', 'version_info', 'warnoptions']
```

Without arguments, `dir()` lists the names you have defined currently:

```python
>>> a = [1, 2, 3, 4, 5]
>>> import fibo
>>> fib = fibo.fib
>>> dir()
['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']
```

Note that it lists all types of names: variables, modules, functions, etc.

`dir()` does not list the names of built-in functions and variables. If you want a list of those, they are defined in the standard module `builtins`:

```python
>>> import builtins
>>> dir(builtins)  
['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException',
 'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning',
 'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError',
 'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning',
 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False',
 'FileExistsError', 'FileNotFoundError', 'FloatingPointError',
 'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError',
 'ImportWarning', 'IndentationError', 'IndexError', 'InterruptedError',
 'IsADirectoryError', 'KeyError', 'KeyboardInterrupt', 'LookupError',
 'MemoryError', 'NameError', 'None', 'NotADirectoryError', 'NotImplemented',
 'NotImplementedError', 'OSError', 'OverflowError',
 'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError',
 'ReferenceError', 'ResourceWarning', 'RuntimeError', 'RuntimeWarning',
 'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError',
 'SystemExit', 'TabError', 'TimeoutError', 'True', 'TypeError',
 'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError',
 'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning',
 'ValueError', 'Warning', 'ZeroDivisionError', '_', '__build_class__',
 '__debug__', '__doc__', '__import__', '__name__', '__package__', 'abs',
 'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable',
 'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits',
 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit',
 'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr',
 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass',
 'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview',
 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property',
 'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice',
 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars',
 'zip']
```

### Packages

Packages are a way of structuring Python’s module namespace by using “dotted module names”. For example, the module name `A.B` designates a submodule named `B` in a package named `A`. Just like the use of modules saves the authors of different modules from having to worry about each other’s global variable names, the use of dotted module names saves the authors of multi-module packages like NumPy or Pillow from having to worry about each other’s module names.

Here’s a possible structure for your package (expressed in terms of a hierarchical filesystem):

```
sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```

When importing the package, Python searches through the directories on `sys.path` looking for the package subdirectory.

The `__init__.py` files are required to make Python treat directories containing the file as packages. This prevents directories with a common name, such as `string`, unintentionally hiding valid modules that occur later on the module search path. In the simplest case, `__init__.py` can just be an empty file, but it can also execute initialization code for the package or set the `__all__` variable.

Users of the package can import individual modules from the package, for example:

```python
import sound.effects.echo
sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
```

An alternative way of importing the submodule is:

```python
from sound.effects import echo
echo.echofilter(input, output, delay=0.7, atten=4)
```

Yet another variation is to import the desired function or variable directly:

```python
from sound.effects.echo import echofilter
echofilter(input, output, delay=0.7, atten=4)
```

Note that when using `from package import item`, the item can be either a submodule (or subpackage) of the package, or some other name defined in the package, like a function, class or variable. The `import` statement first tests whether the item is defined in the package; if not, it assumes it is a module and attempts to load it. If it fails to find it, an `ImportError` exception is raised.

#### Importing * From a Package

When the user writes `from sound.effects import *`, Python goes out to the filesystem, finds which submodules are present in the package, and imports them all. 

If a package’s `__init__.py` code defines a list named `__all__`, it is taken to be the list of module names that should be imported when `from package import *` is encountered. It is up to the package author to keep this list up-to-date when a new version of the package is released.

```python
__all__ = ["echo", "surround", "reverse"]
```

#### Intra-package References

When packages are structured into subpackages, you can also write relative imports, with the `from module import name` form of import statement. These imports use leading dots to indicate the current and parent packages involved in the relative import.

From the `surround`module for example, you might use:

```python
from . import echo
from .. import formats
from ..filters import equalizer
```

Note that relative imports are based on the name of the current module. Since the name of the main module is always `"__main__"`, modules intended for use as the main module of a Python application must always use absolute imports.



## Input and Output

There are several ways to present the output of a program; data can be printed in a human-readable form, or written to a file for future use.

### Fancier Output Formatting

Often you’ll want more control over the formatting of your output than simply printing space-separated values. There are several ways to format output.

#### Formatted String Literals

To use formatted string literals, begin a string with `f` or `F` before the opening quotation mark or triple quotation mark. Inside this string, you can write a Python expression between `{` and `}` characters that can refer to variables or literal values.

```python
>>> year = 2016
>>> event = 'Referendum'
>>> f'Results of the {year} {event}'
'Results of the 2016 Referendum'
```

An optional format specifier can follow the expression. This allows greater control over how the value is formatted. 

```python 
>>> print(f'{name:10} ==> {phone:10d}')
Sjoerd     ==>       4127
>>> print(f'The value of pi is approximately {math.pi:.3f}.')
The value of pi is approximately 3.142.
```

#### The String format() Method

Basic usage of the `str.format()` method looks like this:

```python
>>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
We are the knights who say "Ni!"
```

A number in the brackets can be used to refer to the position of the object passed into the`str.format()` method.

```python
>>> print('{0} and {1}'.format('spam', 'eggs'))
spam and eggs
>>> print('{1} and {0}'.format('spam', 'eggs'))
eggs and spam
```

Expression can be formated as well:

```python
"Weight in tons {0.weight}"       # 'weight' attribute of first positional arg
"Units destroyed: {players[0]}"   # First element of keyword argument 'players'.
```

If keyword arguments are used in the `str.format()` method, their values are referred to by using the name of the argument.

```python
>>> print('This {food} is {adjective}.'.format(
...       food='spam', adjective='absolutely horrible'))
This spam is absolutely horrible.
```

Positional and keyword arguments can be arbitrarily combined:

```python
>>> print('The story of {0}, {1}, and {other}.'.format(
...       'Bill', 'Manfred', other='Georg'))
The story of Bill, Manfred, and Georg.
```

Values in dictionary can be used in format() string as well.

```python
>>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
>>> print('Jack: {Jack}; Sjoerd: {Sjoerd}; Dcab: {Dcab}'.format(**table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678
```

CONFUSED

```python
>>> print('Jack: {[Jack]}; Sjoerd: {[Sjoerd]}; Dcab: {[Dcab]}'.format(table))
Traceback (most recent call last):
	File "<stdin>", line 1, in <module>
IndexError: tuple index out of range
>>> print('Jack: {[Jack]}; Sjoerd: {[Sjoerd]}; Dcab: {[Dcab]}'.format(
...          table, table, table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678
```

#### Manual String Formatting

Besides modify string in format, string can be modified using built-in func()  manually.

The `str.rjust()` method of string objects right-justifies a string in a field of a given width by padding it with spaces on the left. There are similar methods `str.ljust()` and `str.center()`. These methods do not write anything, they just return a new string. There is another method, `str.zfill()`, which pads a numeric string on the left with zeros.

```python
>>> '1' + '2'.rjust(4)
1   2
>>> '1'.ljust(4) + '2'
1   2
>>> '12'.zfill(5)
'00012'
```

### Reading and Writing Files

`open()` returns a file object, and is most commonly used with two arguments.

```python
>>> f = open('workfile', 'w')
```

The first argument is a string containing the filename. The second argument is another string containing a few characters describing the way in which the file will be used. 

```
r	--	read only(default)				w	--	write only
a	--	append							r+ 	-- 	both read and write
```

Normally, files are opened in *text mode*, that means, you read and write strings from and to the file, which are encoded in a specific encoding.  `'b'`appended to the mode opens the file in *binary mode*: now the data is read and written in the form of bytes objects. 

In text mode, the default when reading is to convert platform-specific line endings (`\n` on Unix, `\r\n` on Windows) to just `\n`. When writing in text mode, the default is to convert occurrences of `\n` back to platform-specific line endings. This behind-the-scenes modification to file data is fine for text files, but will corrupt binary data like that in `JPEG` or `EXE` files. **That's why** you should be very careful to use binary mode when reading and writing such files.

It is good practice to use the `with` keyword when dealing with file objects. The advantage is that the file is properly closed after its suite finishes, even if an exception is raised at some point. Using `with` is also much shorter than writing equivalent `try`-`finally` blocks:

```python
>>> with open('workfile') as f:
...     read_data = f.read()
>>> f.closed
True
```

If you’re not using the `with` keyword, then you should call `f.close()` to close the file and immediately free up any system resources used by it. If you don’t explicitly close a file, Python’s garbage collector will eventually destroy the object and close the open file for you, but the file may stay open for a while. 

After a file object is closed, either by a`with` statement or by calling `f.close()`, attempts to use the file object will automatically fail.

```python
>>> f.close()
>>> f.read()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: I/O operation on closed file.
```

#### Methods of File Objects

The rest of the examples in this section will assume that a file object called `f` has already been created.

To read a file’s contents, call `f.read(size)`, which reads some quantity of data and returns it as a string (in text mode) or bytes object (in binary mode).  When *size* is omitted or negative, the entire contents of the file will be read and returned. If the end of the file has been reached, `f.read()` will return an empty string (`''`).

```python
>>> f.read()
'This is the entire file.\n'
>>> f.read()
''
```

`f.readline()` reads a single line from the file; a newline character (`\n`) is left at the end of the string, and is only omitted on the last line of the file if the file doesn’t end in a newline. If `f.readline()` returns an empty string, the end of the file has been reached.

```python
>>> f.readline()
'This is the first line of the file.\n'
>>> f.readline()
'Second line of the file\n'
>>> f.readline()
''
```

For reading lines from a file, you can loop over the file object. This is memory efficient, fast, and leads to simple code:

```python
>>> for line in f:
...     print(line, end='')
...
This is the first line of the file.
Second line of the file
```

If you want to read all the lines of a file in a list you can also use `list(f)` or `f.readlines()`.

`f.write(string)` writes the contents of *string* to the file, returning the number of characters written.

```python
>>> f.write('This is a test\n')
15
```

`f.tell()` returns an integer giving the file object’s current position in the file represented as number of bytes from the beginning of the file when in binary mode and an opaque number when in text mode.

To change the file object’s position, use `f.seek(offset, from_what)`. The position is computed from adding *offset*to a reference point; the reference point is selected by the *from_what* argument. A *from_what* value of 0 measures from the beginning of the file, 1 uses the current file position, and 2 uses the end of the file as the reference point. *from_what* can be omitted and defaults to 0, using the beginning of the file as the reference point.

```python
>>> f = open('workfile', 'rb+')
>>> f.write(b'0123456789abcdef')
16
>>> f.seek(5)      # Go to the 6th byte in the file
5
>>> f.read(1)
b'5'
>>> f.seek(-3, 2)  # Go to the 3rd byte before the end
13
>>> f.read(1)
b'd'
```

In text files (those opened without a `b` in the mode string), only seeks relative to the beginning of the file are allowed (the exception being seeking to the very file end with `seek(0, 2)`) and the only valid *offset* values are those returned from the `f.tell()`, or zero. Any other *offset* value produces undefined behavior.

#### Saving structured data with `json`

Strings can easily be written to and read from a file. Numbers take a bit more effort, since the `read()` method only returns strings, which will have to be passed to a function like [`int()`](https://docs.python.org/3/library/functions.html#int), which takes a string like `'123'` and returns its numeric value 123. When you want to save more complex data types like nested lists and dictionaries, parsing and serializing by hand becomes complicated.

Rather than having users constantly writing and debugging code to save complicated data types to files, Python allows you to use the popular data interchange format called JSON (JavaScript Object Notation). The standard module called `json` can take Python data hierarchies, and convert them to string representations; this process is called *serializing*. Reconstructing the data from the string representation is called *deserializing*. Between serializing and deserializing, the string representing the object may have been stored in a file or data, or sent over a network connection to some distant machine.

If you have an object `x`, you can view its JSON string representation with a simple line of code:

```python
>>> import json
>>> json.dumps([1, 'simple', 'list'])
'[1, "simple", "list"]'
```

To add indents into json string:

```oython
json.dumps(data, sort_keys=True, indent=4, separators=(',', ': '))
```

Another variant of the `dumps()` function, called  `dump()`, simply serializes the object to a text file. So if `f` is a text file object opened for writing, we can do this:

```python
json.dump(x, f)
```

To decode the object again, if `f` is a text file object which has been opened for reading:

```pyhton
x = json.load(f)
```

Or it is a json string:

```python
>>> jsonData = '{"a":1,"b":2,"c":3,"d":4,"e":5}';
>>> json.loads(jsonData)
{'a': 1, 'e': 5, 'd': 4, 'b': 2, 'c': 3}
```



## Errors and Exceptions

There are (at least) two distinguishable kinds of errors: *syntax errors* and *exceptions*.

### Syntax Errors

Syntax errors, also known as parsing errors:

```python
>>> while True print('Hello world')
  File "<stdin>", line 1
    while True print('Hello world')
                   ^
SyntaxError: invalid syntax
```

### Exceptions

Even if a statement or expression is syntactically correct, it may cause an error when an attempt is made to execute it. Errors detected during execution are called *exceptions* and are not unconditionally fatal.

```python
>>> 10 * (1/0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>> 4 + spam*3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'spam' is not defined
>>> '2' + 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't convert 'int' object to str implicitly
```

#### Handling Exceptions

It is possible to write programs that handle selected exceptions.

```python
>>> def divide(x, y):
...     try:
...         result = x / y
...     except ZeroDivisionError:
...         print("division by zero!")
...     else:
...         print("result is", result)
...     finally:
...         print("executing finally clause")
```

The `try` statement works as follows.

- First, the *try clause* (the statement(s) between the `try` and `except` keywords) is executed.
- If no exception occurs, the *except clause* is skipped and execution of the `try` statement is finished.
- If an exception occurs during execution of the try clause, the rest of the clause is skipped. Then if its type matches the exception named after the `except` keyword, the except clause is executed, and then execution continues after the `try` statement.
- If an exception occurs which does not match the exception named in the except clause, it is passed on to outer `try` statements; if no handler is found, it is an *unhandled exception* and execution stops with a message as shown above.
- The `try`… `except` statement has an optional `else` clause, which, when present, must follow all except clauses. It is useful for code that must be executed if the try clause does not raise an exception. 
- The `try`statement has another optional `finally` clause. It is always executed before leaving the [`try`](https://docs.python.org/3/reference/compound_stmts.html#try) statement, whether an exception has occurred or not. 

The test of the above example like this:

```python
>>> divide(2, 1)
result is 2.0
executing finally clause
>>> divide(2, 0)
division by zero!
executing finally clause
>>> divide("2", "1")
executing finally clause
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in divide
TypeError: unsupported operand type(s) for /: 'str' and 'str'
```

A class in an `except` clause is compatible with an exception if it is the same class or a base class thereof.

 An except clause may name multiple exceptions as a parenthesized tuple:

```python
except (RuntimeError, TypeError, NameError):
	pass
```

The last except clause may omit the exception name(s), to serve as a wildcard. Use this with extreme caution, since it is easy to mask a real programming error in this way! It can also be used to print an error message and then re-raise the exception (allowing a caller to handle the exception as well):

```python
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
```

#### Raising Exceptions

The `raise` statement allows the programmer to force a specified exception to occur.

```python
>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
```

The sole argument to `raise` indicates the exception to be raised. This must be either an exception instance or an exception class (a class that derives from `Exception`). If an exception class is passed, it will be implicitly instantiated by calling its constructor with no arguments:

```python
raise ValueError  # shorthand for 'raise ValueError()'
```

If you need to determine whether an exception was raised but don’t intend to handle it, a simpler form of the `raise` statement allows you to re-raise the exception, like the above example:

```python
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
```

User-defined exception can be raised as well. Programs may name their own exceptions by creating a new exception class, typically be derived from the `Exception`class, either directly or indirectly. Exception classes can be defined which do anything any other class can do, but are usually kept simple.

```python
class Error(Exception):
    """Base class for exceptions in this module."""
    pass

class InputError(Error):
    """Exception raised for errors in the input.

    Attributes:
        expression -- input expression in which the error occurred
        message -- explanation of the error
    """

    def __init__(self, expression, message):
        self.expression = expression
        self.message = message

class TransitionError(Error):
    """Raised when an operation attempts a state transition that's not
    allowed.

    Attributes:
        previous -- state at beginning of transition
        next -- attempted new state
        message -- explanation of why the specific transition is not allowed
    """

    def __init__(self, previous, next, message):
        self.previous = previous
        self.next = next
        self.message = message
```

####  Exception arguments

The except clause may specify a variable after the exception name. The variable is bound to an exception instance with the arguments stored in `instance.args`. For convenience, the exception instance defines `__str__()` so the arguments can be printed directly without having to reference `.args`. One may also instantiate an exception first before raising it and add any attributes to it as desired.

```python
>>> try:
...     raise Exception('spam', 'eggs')
... except Exception as inst:
...     print(type(inst))    # the exception instance
...     print(inst.args)     # arguments stored in .args
...     print(inst)          # __str__ allows args to be printed directly,
...                          # but may be overridden in exception subclasses
...     x, y = inst.args     # unpack args
...     print('x =', x)
...     print('y =', y)
...
<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
x = spam
y = eggs
```

 





## 参考文献

1. [The Python Tutorial](https://docs.python.org/3/tutorial/index.html)
2. [[python]list, tuple, dictionary, set的底层细节](https://blog.csdn.net/siyue0211/article/details/80560783)
3. [不可不知的Python模块: collections](https://www.zlovezl.cn/articles/collections-in-python/)
4. [python3 deque（双向队列）的详细介绍](https://www.php.cn/python-tutorials-358240.html)
5. [Python Enclosing作用域、闭包、装饰器话聊上篇](https://segmentfault.com/a/1190000006236947?utm_source=tag-newest)
6. [Python Enclosing作用域、闭包、装饰器话聊下篇](https://segmentfault.com/a/1190000006659077)
7. [简单了解Python装饰器实现原理](https://blog.csdn.net/MonaLisaTearr/article/details/80661937)
8. [装饰器-廖雪峰](https://www.liaoxuefeng.com/wiki/897692888725344/923030163290656)
9. [python生成器yield和send](https://www.cnblogs.com/xhcdream/p/8304953.html)
10. [python函数传参是传值还是传引用？](https://www.cnblogs.com/loleina/p/5276918.html)
11. [Python 函数中，参数是传值，还是传引用？](https://www.cnblogs.com/shizhengwen/p/6972183.html)
12. [比较运算符在Python和C / C ++中的优先级(comparison operators' priority in Python vs C/C++)](http://www.it1352.com/490485.html)
13. [python 多继承与继承原理及多继承中super本质](https://blog.csdn.net/sinat_38068807/article/details/86498814)
14. [][python的动态性和_slot_][python的动态性和_slot_](https://www.cnblogs.com/alexzhang92/p/9416869.html)
15. [Python内存管理机制及优化简析](http://kkpattern.github.io/2015/06/20/python-memory-optimization-zh.html)
16. [从0到1，Python异步编程的演进之路](https://zhuanlan.zhihu.com/p/25228075)
17. [Python Async/Await入门指南](https://zhuanlan.zhihu.com/p/27258289)

