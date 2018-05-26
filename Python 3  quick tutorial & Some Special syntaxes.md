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

---

__Classes__

Class definitions, like function definitions(`def` statements) must be executed before they have any effect. (You could conceivably place a class definition in a branch of an `if` statement. or inside a function.)

When a class defines an `__init__()` method, class instantiation automatically invokes `__init__()` for the newly-created class instance. Of course, the `__init_()`method may have arguments for greater flexibility.

```python
>>> class Complex:
	def __init__(self, realpart, imagpart):
		self.r = realpart
		self.i = imagpart

		
>>> x = Complex(3.0, -4.5)
>>> x.r, x.i
(3.0, -4.5)
```

```python
class MyClass:
    """A simple example calss"""
    i = 12345
    
    def f(self):
        return "Hello World!"
```

Valid method names of an instance object depend on its class. By definition, all attributes of a class that are function objects define corresponding methods of its instances. `x.f` is a valid method reference, since `MyClass.f` is a function, but `x.i` is not, since `MyClass.i` is not. But `x.f` is not the same thing as `MyClass.f` -- it is a method object, not a function object.

In the `MyClass` example, this will return the String `Hello World!`. However, it is not necessary to call a method right away:`x.f` is a method object, and can be stored away and called at a later time.

```python
>>> xf = x.f
>>> print(xf)
Hello World!
```

Python raises an exception when a function that requires an argument is called without any - even if the argument is not actually used...

In general, calling a method with a list of `n` arguments is equivalent to calling the corresponding function with an argument list that is created by inserting the method's instance object before the first argument.

This shared data can have possibly surprising effects with involving [mutable](../glossary.html#term-mutable) objects such as lists and  dictionaries. For example, the *tricks* list in the following code should  not be used as a class variable because just a single list would be shared by  all *Dog* instances: 

```python
class Dog:
    
    tricks = []          # mistaken use of a class variables
    
    def __init__(self, name):
        self.name = name
        
    def add_trick(self, trick):
        self.tricks.append(trick)
        
>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.add_trick('roll over')
>>> e.add_trick('play dead')
>>> d.tricks                # unexpectedly shared by all dogs
['roll over', 'play dead']
```

Correct design of the class should use an instance variable instead:

```python
class Dog:
    
    def __init__(self, name):
        self.name = name
        self.tricks = []
        
    def add_trick(self, trick):
        self.tricks.append(trick)
```

Often, the first argument of a method is called `self`. This is nothing more than a convention: the name `self` has absolutely no special meaning to Python.

When the class object is constructed, the base class is remembered. This is used for resolving attribute references: if a requested attribute is not found in the class, the search proceeds to look in the base class. The rule is applied recursively if the base class itself is derived from some other class.

__Private Variables__

A name prefixed with an underscore (e.g. `_spam`) should be treat as a non-public part of the API (whether it is a function, a method or a data member). It should be considered an implementation detail and subject to change without notice.

---

---

---

__Python Identifiers__

Python is a case sensitive programming language.

Here are naming conventions for Python identifiers:

> * Class names start with an uppercase letter. All other identifiers start with a lowercase letter.
> * Starting an identifier with a single leading underscore indicates that the identifier is private.
> * Starting an identifier with two leading underscores indicates a strong private identifier.
> * If the identifier also ends with two trailing underscores, the identifier is a language-defined special name.

Statements in Python typically end with a new line. Python, however, allows the use of the line continuation character (\\) to denote that the line should continue.

```python
total = item_one + \
    	item_two + \
    	item_therr
```

Python has five standard data type:

> - __Numbers__ -- _Number objects are created when you assign a value to them._
>   - int (signed integers)
>   - float (floating point real values)
>   - complex (complex numbers)
> - __String__ -- _Subsets of strings can be taken using the slice operator `[]` and `[:]`with indexed starting at 0 in  the beginning of the string and working their way from -1 to the end. The plus `+` sign is the string concatenation operator and the asterisk `*` is the repetition operator._
> - __List__ -- _A list contains items separated by commas and enclosed within square brackets `[]`. All the items belonging to a list can be of different data type._ 
> - __Tuple__ -- _A tuple consists of a number of values separated by commas. Unlike lists, however, tuples are enclosed within parenthesis. Lists are enclosed in brackets `[]` and their elements and size can be changed, while tuples are enclosed in parentheses `()` and cannot be updated. Tuples can be thought of as __read-only__ list._
> - __Dictionary__ -- _Python's dictionaries are kind of hash-table type. A dictionary key can be almost any Python type, but are usually numbers or strings. Values, on the other hand, can be any arbitrary Python object. Dictionaries are enclosed by curly braces `{}`. Dictionaries have no concept of order among the elements. They are simply unordered._

To convert between types, you simply use the type-names as a function.

Python's built-in function `bin()` can be used to obtain binary representation of an integer number.

---

To see the list of all modules:

```python
>>> help('modules')

Please wait a moment while I gather a list of all available modules...

__future__          audioop             idle                scrolledlist
__main__            autocomplete        idle_test           search
_ast                autocomplete_w      idlelib             searchbase
_asyncio            autoexpand          imaplib             searchengine
_bisect             base64              imghdr              secrets
_blake2             bdb                 imp                 select
_bootlocale         binascii            importlib           selectors
_bz2                binhex              inspect             setuptools
_codecs             bisect              io                  shelve
_codecs_cn          browser             iomenu              shlex
_codecs_hk          builtins            ipaddress           shutil
_codecs_iso2022     bz2                 itertools           signal
_codecs_jp          cProfile            json                site
_codecs_kr          calendar            keyword             smtpd
_codecs_tw          calltip_w           lib2to3             smtplib
_collections        calltips            linecache           sndhdr
_collections_abc    cgi                 locale              socket
_compat_pickle      cgitb               logging             socketserver
_compression        chunk               lzma                sqlite3
_csv                cmath               macosx              sre_compile
_ctypes             cmd                 macpath             sre_constants
_ctypes_test        code                macurl2path         sre_parse
_datetime           codecontext         mailbox             ssl
_decimal            codecs              mailcap             stackviewer
_distutils_findvs   codeop              mainmenu            stat
_dummy_thread       collections         marshal             statistics
_elementtree        colorizer           math                statusbar
_functools          colorsys            mimetypes           string
_hashlib            compileall          mmap                stringprep
_heapq              concurrent          modulefinder        struct
_imp                config              msilib              subprocess
_io                 config_key          msvcrt              sunau
_json               configdialog        multicall           symbol
_locale             configparser        multiprocessing     symtable
_lsprof             contextlib          netrc               sys
_lzma               copy                nntplib             sysconfig
_markupbase         copyreg             nt                  tabnanny
_md5                crypt               ntpath              tarfile
_msi                csv                 nturl2path          telnetlib
_multibytecodec     ctypes              numbers             tempfile
_multiprocessing    curses              opcode              test
_opcode             datetime            operator            textview
_operator           dbm                 optparse            textwrap
_osx_support        debugger            os                  this
_overlapped         debugger_r          outwin              threading
_pickle             debugobj            paragraph           time
_pyclbr             debugobj_r          parenmatch          timeit
_pydecimal          decimal             parser              tkinter
_pyio               delegator           pathbrowser         token
_random             difflib             pathlib             tokenize
_sha1               dis                 pdb                 tooltip
_sha256             distutils           percolator          trace
_sha3               doctest             pickle              traceback
_sha512             dummy_threading     pickletools         tracemalloc
_signal             dynoption           pip                 tree
_sitebuiltins       easy_install        pipes               tty
_socket             editor              pkg_resources       turtle
_sqlite3            email               pkgutil             turtledemo
_sre                encodings           platform            types
_ssl                ensurepip           plistlib            typing
_stat               enum                poplib              undo
_string             errno               posixpath           unicodedata
_strptime           faulthandler        pprint              unittest
_struct             filecmp             profile             urllib
_symtable           fileinput           pstats              uu
_testbuffer         filelist            pty                 uuid
_testcapi           fnmatch             py_compile          venv
_testconsole        formatter           pyclbr              warnings
_testimportmultiple fractions           pydoc               wave
_testmultiphase     ftplib              pydoc_data          weakref
_thread             functools           pyexpat             webbrowser
_threading_local    gc                  pyparse             windows
_tkinter            genericpath         pyshell             winreg
_tracemalloc        getopt              query               winsound
_warnings           getpass             queue               wsgiref
_weakref            gettext             quopri              xdrlib
_weakrefset         glob                random              xml
_winapi             grep                re                  xmlrpc
abc                 gzip                redirector          xxsubtype
aifc                hashlib             replace             zipapp
antigravity         heapq               reprlib             zipfile
argparse            help                rlcompleter         zipimport
array               help_about          rpc                 zlib
ast                 history             rstrip              zoomheight
asynchat            hmac                run                 zzdummy
asyncio             html                runpy               
asyncore            http                runscript           
atexit              hyperparser         sched               

Enter any module name to get more help.  Or, type "modules spam" to search
for modules whose name or summary contain the string "spam".
```

---

__String__

Python does not support a character type; these are treated as strings of length one, thus also considered a substring.

---

__Tuples__

To write a tuple containing a single value you have to include  a comma, even though there is only one value

```python
>>> tup = (1,)
(1,)
```

Tuples are immutable, which means you cannot update or change the values of tuple elements. You are able to tale portions of the exiting tuples to create new tuples as the following example demonstrates.

No enclosing Delimiters is any set of multiple objects, comm-separated, written with out identifying symbols, i.e., brackets for lists, parentheses for tuples, etc.

More than one entry per key is not allowed. This means no duplicate key is allowed. When duplicate keys are encountered during assignment, the last assignment wins.

```python
>>> dict1 = {"Name":"Alice", "Name":"Mary"}
>>> dict1
{'Name': 'Mary'}
```

Keys must be immutable. This means you can use strings, numbers or tuples as dictionary keys but something like ['key'] is not allowed.

---

__The Anonymous Functions__

You can use the __lambda__ keyword to create small anonymous functions.

> - Lambda forms can take any number of arguments but return just one value in the form of an expression. They cannot contain commands or multiple expressions.
> - An anonymous function cannot be a direct call to print because lambda requires an expression.
> - Lambda functions have their own local namespace and cannot access variables other than those in their parameter list and those in the global namespace.
> - Although it appears that lambdas are one-line version of a function, they are not equivalent to inline statements in C or C++, whose purpose is to stack allocation by passing function, during invocation for performance reasons.

The syntax of __lambda__ functions contains only a single statement, which is as follows

```python
lambda [arg1 [,arg2, ...... argn]]: expression
```

```python
>>> sum = lambda arg1, arg2 : arg1 + arg2
>>> sum (1, 2)
3
>>> sum ("Py", "thon")
"Python"
```

---

__The assert Statement__

When it encounters an assert statement, Python evaluates the accompanying expression, which is hopefully true. If the expression is false, Python raises an `AssertionErro` exception.

The syntax for assert is

```python
assert Expression[, Arguments]
```

If the assertion fails, Python uses `ArgumentExpression` as the argument for the `AssertionError`. `AssertionError` exceptions can be caught and handled like any other exception, using the try-except statement. If they are not handled, they will terminate the program and produce a traceback.

```
def test(n):
	assert n >= 0, "The `n` must not be negtive."
	pass
```

---

Here are few important points about the above-mentioned syntax:

> - A single `try` statement can have multiple except statements. This is useful when the try block contains statements that may throw different types of exceptions.
> - You can also provide a generic except clause, which handles any exception.
> - After the except clause(s), you can include an `else-clause`. The code in the `else-block` executes if the code in the `try`: block does not raise an exception.
> - The `else-block` is a good place for code that does not need the `try`: block's protection.



Examples:

```python
try:
    # You do your operations here.
    
except:
    # If there is any exception, then execute this block.
    
else:
    # If there is no exception then execute this block.
```

```python
try:
    # You do your operations here.
    ......
    # Due to any exception, this may be skipped.
finally:
    # This would always be executed.
```

__Note__: You can provide `except` clause(s), or a `finally` clause, but not both. You can not use `else` clause as well along with a `finally` clause.

An exception can have an _argument_, which is a value that gives additional information about the problem.

```python
try:
    # Do your operations here.
except ExceptionType as Argument:
    # You can print value of Argument here...
```

If you are trapping multiple exceptions, you can have a variable follow the tuple of the exception. The variable can receive a single value or multiple values in the form of a tuple. This tuple usually contains the error string, the error number, and an error location.

You can raise exceptions in several ways by using the `raise` statement.

```python
raise [Exception [, args [, traceback]]]
```

Here, _Exception_ is the type of exception (for example, NameError) and _argument_ is value for the exception argument. The argument is optional; if not supplied, the exception argument is __None__.

Python also allows you to create your own exceptions by deriving classed from the standard built-in exceptions.

```python
class NetworkError(RuntimeError):
    """"""
    
    def __init__(self, args):
        self.args = args
```

Usage:

```python
try:
    rasie NetworkError("Bad hostname")
except NetworkError as err:
    print(err.args)
```

---

__Overloading Operators__

You could, however, define the *\_\_add__* method  in your class, and then the plus operator would behave as per expectation.

___You need to name attributes with a double underscore prefix, and those attributes the will not be directly visible to outsides.___

> Python protects those members by internally changing the name to include the class name. You can access such attributes as `object._className__attrName`.

---

__Regular Expressions__

The __re__ module raises the exception __re.error__ if an error occurs while compiling or using a regular expression. To avoid any confusion while dealing with regular expressions, we would use Raw String as __r'expression'__.

Basic patterns that match single chars:

| Expression   | Matches                                                      |
| ------------ | ------------------------------------------------------------ |
| a, X, 9, <   | ordinary characters just match themselves exactly.           |
| . (a period) | matches any single character except newline `\n`.            |
| \w           | matches a "word" character: a letter or digit or under-bar `[a-zA-Z0-9_]`. |
| \W           | matches any non-word character.                              |
| \b           | boundary between word and non-word.                          |
| \s           | matches a single whitespace character: space, newline, return, tab. |
| \S           | matches any non-whitespace character.                        |
| \t, \n, \r   | tab, newline, return.                                        |
| \d           | decimal digit `[0-9]`.                                       |
| ^            | matches start of the string.                                 |
| $            | match the end of the string.                                 |
| \            | inhibit the "specialness" of a character.                    |

Compilation flags

| Flag          | Meaning                                                      |
| ------------- | ------------------------------------------------------------ |
| A, ASCII      | Make several escapes like `\w, \b, \s,\d ` match only on ASCII characters with the respective property. |
| S, DOTALL     | Make, match any character, including newlines.               |
| I, IGNORECASE | Do case-insensitive matches.                                 |
| L, LOCALE     | Do a locale-aware match.                                     |
| M, MULTILINE  | Multi-line matching, affecting ^ and $.                      |
| X, VERBOSE    | Enable verbose REs, which can be organized more cleanly and understandably. |

`match` checks for a match only at the beginning of the string, while `search` checks for a match anywhere in the string:

```python
#!/usr/bin/python3
import re

line = "Cats are smarter than dogs";

matchObj = re.match( r'dogs', line, re.M|re.I)
if matchObj:
   print ("match --> matchObj.group() : ", matchObj.group())
else:
   print ("No match!!")

searchObj = re.search( r'dogs', line, re.M|re.I)
if searchObj:
   print ("search --> searchObj.group() : ", searchObj.group())
else:
   print ("Nothing found!!")
```

This will print:

```python
No match!!
search --> searchObj.group() :  dogs
```

List of regular expression syntax in Python:

| Parameter   | Description                                                | Parameter    | Description                                                 |
| ----------- | ---------------------------------------------------------- | ------------ | ----------------------------------------------------------- |
| ^           | beginning of line                                          | $            | end of line                                                 |
| .           | any single character except newline                        | [...]        | any single character in brackets                            |
| [^...]      | any single character not in brackets                       | `re`*        | 0 or more occurrences of preceding expression               |
| `re`+       | 1 or more occurrences of preceding expression              | `re`?        | 0 or 1 occurrence of preceding expression                   |
| `re`{n}     | n number of occurrences of preceding expression            | `re`{n,}     | n or more occurrences of preceding expression               |
| `re`{n,m}   | least n and most n occurrences of preceding expression     | a\|b         | either a or b                                               |
| (`re`)      | groups regular expressions and remembers matched text      | (?imx)       | toggles on i, m, or x options within a regular expression   |
| (?-imx)     | toggles off i, m, or x options within a regular expression | (?:`re`)     | groups regular expressions without remembering matched text |
| (?imx:`re`) | toggles on i, m, or x options within parentheses           | (?-imx:`re`) | toggles off i, m, or x options within parentheses           |
| (?#...)     | comment                                                    | (?=`re`)     | specifies position using a pattern                          |
| (?!`re`)    | specifies position using pattern negation                  | (?>`re`)     | independent pattern without backtracking                    |
| \w          | word characters                                            | \W           | non-word characters                                         |
| \s          | whitespace,`[\t\n\r\f]`                                    | \S           | non-whitespace                                              |
| \d          | [0-9]                                                      | \D           | non-digits                                                  |
| \A          | beginning of string                                        | \Z,\z        | end of string                                               |
| \G          | point where last match finished                            | \b           | word boundaries                                             |
| \B          | non-boundaries                                             | \n, \t, etc  | newline, carriage return, tabs, etc                         |
| \1...\9     | nth grouped subexpression                                  | \10          |                                                             |

---

__CGI (Common Gateway Interface)__

> CGI Architecture Diagram

> ![cgiarch](https://www.tutorialspoint.com/python/images/cgiarch.gif)

[>>> See More](https://www.tutorialspoint.com/python3/python_cgi_programming.htm)

---

