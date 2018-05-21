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



