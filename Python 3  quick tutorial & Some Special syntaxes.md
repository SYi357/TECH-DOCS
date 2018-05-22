# Python 3  quick tutorial & Some Special syntaxes

```python
>>> 8 / 5 # division always returns a floating point number
1.6
>>> 17 / 3 # classic division returns a float
5.666666666666667
>>> 17 // 3 # floor division discards the fractional part
5
>>> 17 % 3 # the % operator returns the remainder of the division
2
>>> 5 ** 2 # 5 squared
25
>>> 2 ** 7 # 2 to the power of 7
128
```

__In interactive mode__, the last printed expression is assigned to the variable  `_`, which should be treated as read-only by the user.

Python also has built-in support for __complex numbers__, and user the `j` or 	`J` suffix to indicate the imaginary part (e.g. `3 + 5j`).

---

Python can also manipulate strings, which can be expressed in several ways. They can be enclosed in single quotes (`'...'`) or double quotes (`"..."`) with the same results.

If you don't want characters prefaced by `\` to be interpreted as special characters, you can use _raw settings_ by adding an `r` before the first quote:

```python
>>> print (r'C:\some\name')
```

String can be concatenated (glued together) with the `+` operator, and repeated with `*`:

```python
>>> # 3 time 'o', followed by ' cool!'
>>> 'S' + (3 * 'o') + ' cool!'
'Sooo cool!'
```

Two or more *string literals* (i.e. the ones enclosed between quotes)  next to each other are automatically concatenated. This only works with two literals though, not with variables or expressions. You just use `+` to concatenate variables or a variable an a literal.

```python
>>> 'Py' 'thon'
'Python'
>>>
>>> text = ('Put several strings within parentheses '
            'to have them joined together.')
>>> text
'Put several strings within parentheses to have them joined together.'
```

Slice indices have useful defaults; an omitted first index defaults to zero, an omitted second index defaults to the size of the string being sliced.

> __Note__: The `s[:i] + s[i:]` is always equal to `s`.

```python
>>> word = 'Python'
>>> word[:2]   # character from the beginning to position 2 (excluded)
'Py'
>>> word[4:]   # characters from position 4 (included) to the end
'on'
>>> word[-2:]  # characters from the second-last (included) to the end
'on'
```

> __Note__: Python strings cannot be changed - they are immutable. Therefore, assigning to an indexed position in the string results in an error.

If you need a different string, you should create a new one:

```python
>>> 'J' + word[1:]
'Jython'
>>> word[:2] + 'py'
'Pypy'
```

---

Unlike strings, which are immutable, lists are a mutable type, i.e. it is possible to change their content.   Assignment to slices is also possible, and this can even change the size of the list or clear it entirely:

```python
>>> letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> letters
['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> # replace some values
>>> letters[2:5] = ['C', 'D', 'E']
>>> letters
['a', 'b', 'C', 'D', 'E', 'f', 'g']
>>> # now remove them
>>> letters[2:5] = []
>>> letters
['a', 'b', 'f', 'g']
>>> # clear the list by replacing all the elements with an empty list
>>> letters[:] = []
>>> letters
[]
```

---

A line could contain a multiple assignment, just like this:

```python
>>> a, b = 0, 1
```

The variables `a` and `b` simultaneously get the new values 0 and 1.

> Example:
>
> ```python
> >>> a, b = 0, 1
> >>> while b < 1000:
> 	print (b, end = ',')
> 	a, b = b, (a + b)
> 
> 	
> 1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,
> ```

---

The `pass` statement does nothing. It can be used when a statement is required syntactically but the program requires no action. For example:

```python
>>> while True:
    pass # Busy-wait for keyboard interrupt (Ctrl + C)
```

This is commonly used for creating minimal classes:

```python
>>> class MyClass:
    pass
```

Another place `class` can be used is as a place-holder for a function or conditional body when you are working on new code, allowing you to keep thinking at a more abstract level. The `pass` is silently ignored:

```python
>>> def initLog (*args):
    pass # Remember to implement this!
```

---

The `return` statement returns with a value from a function. `return` without an expression argument returns `None`. Falling off the end of a function also returns `None`.

---

__Important warning__: The default value is evaluated only once. This makes a difference when the default is a mutable object such as a list, dictionary, or instances of most classes. For example, the following function accumulates the arguments passed to it on subsequent calls:

```python
def f (a, L=[]):
    L.append(a)
    return L

print (f(1))
print (f(2))
print (f(3))
```

This will print

```python
[1]
[1, 2]
[1, 2, 3]
```

If you do not want the default to be shared between subsequent calls, you can write the function like this instead:

```python
de f (a, L = None):
    if L is None:
        L = []
    L.append (a)
    return L
```

---

When a final formal parameter of the form `**name` is present, it receives a dictionary containing all keyword arguments except for those corresponding to a formal parameter. This  may be combined with a formal parameter of the form `*name` which receives a tuple containing the positional arguments beyond the formal parameter list. (`*name` must occur before `**name`.) For example:

```python
def cheeseshop(kind, *arguments, **keywords):
    print("-- Do you have any", kind, "?")
    print("-- I'm sorry, we're all out of", kind)
    for arg in arguments:
        print(arg)
    print("-" * 40)
    for kw in keywords:
        print(kw, ":", keywords[kw])

cheeseshop("Limburger", "It's very runny, sir.",
           "It's really very, VERY runny, sir.",
           shopkeeper="Michael Palin",
           client="John Cleese",
           sketch="Cheese Shop Sketch")    
```

---

Here is an example of a multi-line docstring:

```python
def my_function ():
    """Do nothing, but document it.
    
    No, really, it doesn't do anything.
    """
    pass

print (my_function.__doc__)
```

The first line should always be a short, concise summary of the object’s purpose. For brevity, it should not explicitly state the object’s name or type, since these are available by other means (except if the name happens to be a verb describing a function’s operation). This line should begin with a capital letter and end with a period.
If there are more lines in the documentation string, the second line should be blank, visually separating the summary from the rest of the description. The following lines should be one or more paragraphs describing the object’s calling conventions, its side effects, etc.

---

__Function annotations__ are completely optional metadata information about the types used by user-defaulted functions.

Annotations are stored in the `__annotations__`  attribute of the function as a dictionary and have no effect on any other part of the function.

---

__Coding Style__

> * Use 4-space indentation, and no tabs.
>   4 spaces are a good compromise between small indentation (allows greater nesting depth) and large indentation (easier to read). Tabs introduce confusion, and are best left out.
> * Wrap lines so that they don’t exceed 79 characters.
>   This helps users with small displays and makes it possible to have several code files side-by-side on larger displays.
> * Use blank lines to separate functions and classes, and larger blocks of code inside functions.
> * When possible, put comments on a line of their own.
> * Use doc-strings.
> * Use spaces around operators and after commas, but not directly inside bracketing constructs:`a = f(1, 2) + g(3, 4)`.
> * Name your classes and functions consistently; the convention is to use `CamelCase` for classes and `lower_case_with_underscores` for functions and methods. Always use `self` as the name for the first method argument (see A First Look at Classes for more on classes and methods).
> * Don’t use fancy encodings if your code is meant to be used in international environments. Python’s default, UTF-8, or even plain ASCII work best in any case.
> * Likewise, don’t use non-ASCII characters in identifiers if there is only the slightest chance people speaking a different language will read or maintain the code.

---

__zip()__ function:

```python
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
]

print(matrix)
matrix2 = list(zip(*matrix))
```

This will print

```python
[[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]]
[(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)]
```

---

A tuple consists of a number of values separated by commas, for instance:

```python
t = 1234, 5, 6789, 'hello!'
u = t, ('A', 'B', 'C')

print (t, '\n', u, '\n', len(t), ', ', len(u))
```

This will print

```python
(1234, 5, 6789, 'hello!') 
 ((1234, 5, 6789, 'hello!'), ('A', 'B', 'C'))
 4, 2
```

---

Python also includes a data type for sets. A set is an unordered collection with no duplicate elements. Basic uses include membership testing and eliminating duplicate entries. Set objects also support mathematical operations like union, intersection, difference, and symmetric difference.

```python
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
{'r, d'}
```

---

The `dict()` constructor builds dictionaries directly from sequences of key-value pairs:

```python
>>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
{'sape': 4139, 'jack': 4098, 'guido': 4127}
>>> dict(sape=4139, guido=4127, jack=4098)
{'sape': 4139, 'jack': 4098, 'guido': 4127}
```

---

__Modules__

In Python, a file is called a _module_; definitions from a module can be imported into other modules or into the _main_ module(the collection of variables that you have access to in a script executed at the top level and in calculator mode).

When you run a Python module with

```python
python fibo.py <arguments>
```

the code in the module will be executed, just as if you imported it, bu with the `__name__` set to `__main__`. That means that by adding this code at the end of your module:

```python
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```

you can make the file usable as a script as well ad importable module, because the code that parses the command line only runs if the module is executed as the "main" file:

```python
python fibo.py 50
1 2 3 5 8 13 21 34
```

If the module id imported, the code is not run:

```python
import fibo
```

This is often used either to provide a convenient user interface to module, or for testing purposes(running the module as a script executes a test suite).

---

The built-in function `dir()` is used to find out which names a module defines. It returns a sorted list of strings.

Without arguments, `dir()` lists the names you have defined currently.

Note that it lists all types of names: variables, modules, functions, etc.

`dir(builtins)` does list the names of built-functions and variables.

```python
>>> import builtins
>>> dir(builtins)
['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException', 'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning', 'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError', 'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning', 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False', 'FileExistsError', 'FileNotFoundError', 'FloatingPointError', 'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError', 'ImportWarning', 'IndentationError', 'IndexError', 'InterruptedError', 'IsADirectoryError', 'KeyError', 'KeyboardInterrupt', 'LookupError', 'MemoryError', 'ModuleNotFoundError', 'NameError', 'None', 'NotADirectoryError', 'NotImplemented', 'NotImplementedError', 'OSError', 'OverflowError', 'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError', 'RecursionError', 'ReferenceError', 'ResourceWarning', 'RuntimeError', 'RuntimeWarning', 'StopAsyncIteration', 'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError', 'SystemExit', 'TabError', 'TimeoutError', 'True', 'TypeError', 'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError', 'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning', 'ValueError', 'Warning', 'WindowsError', 'ZeroDivisionError', '__build_class__', '__debug__', '__doc__', '__import__', '__loader__', '__name__', '__package__', '__spec__', 'abs', 'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable', 'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits', 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit', 'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr', 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass', 'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview', 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property', 'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice', 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars', 'zip']
```

---

It is good practice to use the `with` keyword when dealing with file objects. The advantage is that the file id properly closed its suite finishes, even if an exception is raised at some point. Using `with` is also much shorter than writing equivalent `try-finally` blocks:

```python
with open('workfile') as f:
    ...
```

---

__Handing Exceptions__

It is possible to write programs that handle selected exceptions.

```python
def func:
    try:
        ...
    except (ValueError, RuntimeError, TypeError, ...):
        ...
    except OSError:
        ...
    else:
        ...
```

The use of the else clause is better than adding additional code to the try clause because it avoids accidentally catching an exception that was not raised by the code being protected by the try … except statement.

The `try` statement works as follows:

* First, the `try` clause (the statement(s) between the `try` and `except` keywords) is executed. 

* If no exception occurs, the except clause is skipped and execution of the `try` statement is finished. 

* If an exception occurs during execution of the `try` clause, the rest of the clause is skipped. Then if its type matches the exception named after the `except` keyword, the `except` clause is executed, and then execution continues after the `try` statement.

* If an exception occurs which does not match the exception named in the except clause, it is passed on to outer `try` statements; if no handler is found, it is an unhandled exception and execution stops with a message as the below cases. 

  > ```python
  > >>> 10 * (1/0)
  > Traceback (most recent call last):
  >   File "<stdin>", line 1, in <module>
  > ZeroDivisionError: division by zero
  > >>> 4 + spam*3
  > Traceback (most recent call last):
  >   File "<stdin>", line 1, in <module>
  > NameError: name 'spam' is not defined
  > >>> '2' + 2
  > Traceback (most recent call last):
  >   File "<stdin>", line 1, in <module>
  > TypeError: Can't convert 'int' object to str implicitly
  > ```

For convenience, the exception instance defines `__str__()` so the arguments can be printed directly without having to reference `.args`.

```python
def func():
    try:
        rasie Exception('spam', 'eggs')
    except Exception as inst:
        print(inst.args)     # arguments stored in .args.
        print(inst)          # __str__ allows args to be printed directly,
                             # but may be overridden in exception subclasses
                             # unpack args.
```

User-defined Exceptions:

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

