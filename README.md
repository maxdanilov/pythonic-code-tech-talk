# 🐍 Python: Tips & Tricks

## How to Write More Pythonic Code

- [🐍 Python: Tips & Tricks](#-python-tips--tricks)
  - [How to Write More Pythonic Code](#how-to-write-more-pythonic-code)
- [🪷 Zen of Python](#-zen-of-python)
- [📝 Python History](#-python-history)
- [🎻 String Formatting](#-string-formatting)
  - [The Simple (`+`)](#the-simple-)
  - [The Old (`%`)](#the-old-)
  - [The Meh (`.format`)](#the-meh-format)
  - [The Good (`f-strings`)](#the-good-f-strings)
- [🌱 Basic Data Structures](#-basic-data-structures)
  - [Lists](#lists)
    - [Iteration](#iteration)
    - [Math Operations](#math-operations)
    - [List Slicing `[::]`](#list-slicing-)
    - [Membership Testing With `in`](#membership-testing-with-in)
    - [List Comprehension](#list-comprehension)
    - [Mapping and Filtering](#mapping-and-filtering)
    - [Sorting Lists](#sorting-lists)
    - [Truthiness](#truthiness)
    - [Flatten List of lists](#flatten-list-of-lists)
  - [Strings](#strings)
    - [Membership Check With `in`](#membership-check-with-in)
    - [Stripping Whitespace Characters](#stripping-whitespace-characters)
    - [Prefix/Suffix Manipulations](#prefixsuffix-manipulations)
    - [Tokenization](#tokenization)
  - [Dicts](#dicts)
    - [Iteration](#iteration-1)
    - [Membership Check With `in`](#membership-check-with-in-1)
    - [Dict Comprehension](#dict-comprehension)
    - [Accessing Values: `[]` vs. `get`](#accessing-values--vs-get)
    - [Safe Navigation](#safe-navigation)
    - [Merging](#merging)
  - [Tuples](#tuples)
  - [Sets](#sets)
- [🧑‍🔧 Data Structures: Examples](#-data-structures-examples)
  - [🦄 Get Unique Elements of a List](#-get-unique-elements-of-a-list)
  - [🔍 Search in a List of Objects](#-search-in-a-list-of-objects)
  - [🪡 Is Any of the Values](#-is-any-of-the-values)
- [📦 Values Unpacking](#-values-unpacking)
  - [🔁 Variable Swapping](#-variable-swapping)
  - [📭 Unpacking With Lists and Tuples](#-unpacking-with-lists-and-tuples)
- [🌾 Data Classes](#-data-classes)
- [🦆 Type Hinting](#-type-hinting)
  - [Basic Type Hinting](#basic-type-hinting)
  - [Type Hinting & Multiple Types](#type-hinting--multiple-types)
  - [Type Hinting & Containers](#type-hinting--containers)
  - [Type Hinting & Generic Objects](#type-hinting--generic-objects)
  - [Type Hinting and Local Variables](#type-hinting-and-local-variables)
- [👷‍♂️ Operators](#️-operators)
  - [👯‍♀️ Double Comparison](#️-double-comparison)
  - [🧬 Pattern Matching](#-pattern-matching)
  - [🍴 Ternary Operator](#-ternary-operator)
  - [🦷 Walrus Operator `:=`](#-walrus-operator-)
  - [🛂 `==` vs `is`](#--vs-is)
    - [Copying an Object](#copying-an-object)
- [🧮 Named Parameters](#-named-parameters)
- [🏀 Practical Examples](#-practical-examples)
  - [📁 Reading/Writing Files](#-readingwriting-files)
  - [🅾️ Loading/Exporting JSON](#️-loadingexporting-json)
    - [Reading JSON Files](#reading-json-files)
  - [🌍 HTTP Requests](#-http-requests)
- [🔨 Tools](#-tools)
  - [🔁 REPL](#-repl)
  - [🐞 Debugging](#-debugging)
- [🏁 Outro: Key Advice](#-outro-key-advice)
- [🙇‍♂️ Thank You!](#️-thank-you)

---

# 🪷 Zen of Python

```python
import this
```
```text
>>> The Zen of Python, by Tim Peters

>>> Beautiful is better than ugly.
>>> Explicit is better than implicit.
>>> Simple is better than complex.
>>> Complex is better than complicated.
>>> Flat is better than nested.
>>> Sparse is better than dense.
>>> Readability counts.
>>> Special cases aren't special enough to break the rules.
>>> Although practicality beats purity.
>>> Errors should never pass silently.
>>> Unless explicitly silenced.
>>> In the face of ambiguity, refuse the temptation to guess.
>>> There should be one-- and preferably only one --obvious way to do it.
>>> Although that way may not be obvious at first unless you're Dutch.
>>> Now is better than never.
>>> Although never is often better than *right* now.
>>> If the implementation is hard to explain, it's a bad idea.
>>> If the implementation is easy to explain, it may be a good idea.
>>> Namespaces are one honking great idea -- let's do more of those!
```

---

# 📝 Python History

- [3.6](https://realpython.com/python36-new-features/) (Dec 23, 2016): f-strings
- [3.7](https://realpython.com/python37-new-features/) (Jun 27, 2018): data classes
- [3.8](https://realpython.com/python38-new-features/) (Oct 14, 2019): walrus operator
- [3.9](https://realpython.com/python39-new-features/) (Oct 5, 2020): simpler dictionary updates/merges
- [3.10](https://realpython.com/python310-new-features/) (Oct 4, 2021): pattern matching
- [3.11](https://deepsource.io/blog/python-3-11-whats-new/) (Oct 3, 2022): performance increases (~25%)
  
---

# 🎻 String Formatting

There are 4 ways to do that in Python, with a single preferred one.

---

## The Simple (`+`)

🚫 Plain approach to glue strings together:

```python
name = "Bob"
greeting = "hello"
message = greeting + " there, " + name + "!"
message
>>> 'hello there, Bob!'
```

ℹ️ One can only concatenate strings with strings:

```python
units = 10
items = "apples"
print("Currently in stock: " + str(units) + " " + items)
>>> 'Currently in stock: 10 apples'
```

---

## The Old (`%`)

🚫

```python
name = "Bob"
greeting = "hello"
message = "%s there, %s!" % (greeting, name)
message
>>> 'hello there, Bob!'

# same result:
message = "%(greeting)s, %(name)s!" % {"greeting": greeting, "name": name}
```

---

## The Meh (`.format`)

🚫

```python
name = "Bob"
greeting = "hello"
message = "{} there, {}!".format(greeting, name)
message
>>> 'hello there, Bob!'

# can enumerate params:
message = "{0} there, {1}!".format(greeting, name)
message = "{1} there, {0}!".format(name, greeting)
>>> 'hello there, Bob!'

# same result:
message = "{greeting} there, {name}!".format(greeting=greeting, name=name)
```

---

## The Good (`f-strings`)

Added in Python 3.6:

✅ Looks better, more powerful, better performance (2x faster than `format`, 50% faster than `%`):

```python
name = "Bob"
greeting = "hello"
message = f"{greeting} there, {name}!"

message
>>> 'hello there, Bob!'
```

---

ℹ️ Any Python expressions and value [formatting](https://docs.python.org/3/library/string.html#format-specification-mini-language) support:
```python
import math

r = 2

print(f"Circle of radius {r} has a circumference of {2 * math.pi * r}")
>>> Circle of radius 2 has a circumference of 12.566370614359172

print(f"Circle of radius {r} has a circumference of {2 * math.pi * r:.2f}")
>>> Circle of radius 2 has a circumference of 12.57
``` 

---

ℹ️ Debugging specifier `=` (added in Python 3.8):
```python
x = 123; y = 456
print(f"Calculated values: x={x}, y={y}")
>>> Calculated values: x=123, y=456
print(f"Calculated values: {x=}, {y=}")
>>> Calculated values: x=123, y=456

data = {'city': 'Berlin', 'country': 'DE'}
print(f"Result: {data=}")
>>> Result: data={'city': 'Berlin', 'country': 'DE'}
```

---

# 🌱 Basic Data Structures

---

- Lists
- Strings
- Dicts
- Tuples
- Sets

---

## Lists

---

A list is a **mutable**, **ordered** array of values

```python
data = [1, 3, 5]
data.append(7)
data
>>> [1, 3, 5, 7]
data.extend([9, 11])  # same as: data += [9, 11]
>>> [1, 3, 5, 7, 9, 11]
len(data)
>>> 6
```

---

### Iteration

🚫 Index-based iteration loops:
```python
for i in range(len(data)):
    print(data[i])
>>> 1
>>> 3
>>> 5
```

✅ Every list is [iterable](https://www.pythonlikeyoumeanit.com/Module2_EssentialsOfPython/Iterables.html):

```python
for x in data:
    print(x)
>>> 1
>>> 3
>>> 5
```

---

ℹ️ In case one needs to access the current element's index:

```python
for i, x in enumerate(data):
    print(f"Element {i}: {x}")
>>> Element 0: 1
>>> Element 1: 3
>>> Element 2: 5
```

---

### Math Operations

🚫 

```python
data = [1, 2, -3, 4, 5]
sum_ = 0
min_ = data[0]
max_ = data[0]
for x in data:
    sum_ += x
    if x < min_:
        min_ = x
    if x > max_:
        max_ = x

sum_
>>> 9
min_
>>> -3
max_
>>> 5
```

---

✅

```python
data = [1, 2, -3, 4, 5]
sum(data)
>>> 9
min(data)
>>> -3
max(data)
>>> 5
```

---

### List Slicing `[::]`

Done with so-called 🍣 sushi-operator (`[::]`):
```
array[<start_index>:<stop_index>:<step>]
```

- `start_index` = `0` if not specified
- `stop_index` = `len(array)` if not specified
  - it's exclusive: `stop_index` value is **not** included in the slice result
- `step_index` = `1` if not specified

---

```python
data =    [2, 4, 6, 8, 10]
# index:   0  1  2  3  4
data[1:]  # same as [1::] or [1:5:1]
>>> [4, 6, 8, 10]
data[1:3] # same as [1:3:1]
>>> [4, 6]
data[::2] # same as [0:5:2]
>>> [2, 6, 10]

data == data[0:5:1]
>>> True
data == data[:]
>>> True
```

Slicing the full list with step `-1` (backwards) returns a reversed version of the list:
```python
data = [2, 4, 6, 8, 10]
data[::-1]
>>> [10, 8, 6, 4, 2]
```

---

### Membership Testing With `in`

🚫 Implement searching algorithm yourself:

```python
array = [1, 2, 3, 4, 5]
search_for = 3
found = False
for i in range(len(array)):
    if array[i] == search_for:
        found = True
        break
print(f"Found: {found}")
>>> True
```

✅ Let Python do it:

```python
array = [1, 2, 3, 4, 5]
search_for = 3
found = search_for in array
print(f"Found: {found}")
>>> True
```

---

### List Comprehension

Formula: `[value for item in iterable]` (for every `item` in `iterable` map it to `value`)

```python
# range(A, B, C) = iterator of integer sequence from A to B with a step C (B is excluded) 
data = [x ** 2 for x in range(0, 5)]
data
>>> [0, 1, 4, 9, 16]
```

List comprehension with a condition (formula: `[value for item in iterable if condition]`)

```python
data = [3, 2, -5, 10, 21, 7]
even = [x for x in data if x % 2 == 0]
even
>>> [2, 10]
```

---

### Mapping and Filtering

Alternative to list comprehension is to use `map` (with a [lambda function](https://realpython.com/python-lambda/) (inline function))

```python
data = map(lambda x: x ** 2, range(0, 5))

print(list(data))  # `map` returns an iterator, `list` creates a materialized list of it
>>> [0, 1, 4, 9, 16]
```

Alternative to list comprehension with a condition is to use `filter` (with a [lambda function](https://realpython.com/python-lambda/) (inline function)):

```python
data = [3, 2, -5, 10, 21, 7]
even = filter(lambda x: x % 2 == 0, data)
list(even)  # `filter` returns an iterator, `list` creates a materialized list of it
>>> [2, 10]
```

---

### Sorting Lists

```python
data = [
  {'city': 'Paris', 'country': 'FR'},
  {'city': 'Berlin', 'country': 'DE'},
  {'city': 'London', 'country': 'UK'}
]

# order by city name:
sorted(data, key=lambda x: x['city'])
>>> [{'city': 'Berlin', 'country': 'DE'}, {'city': 'London', 'country': 'UK'}, {'city': 'Paris', 'country': 'FR'}]

# order by country code reversed:
sorted(data, key=lambda x: x['country'], reverse=True)
>>> [{'city': 'London', 'country': 'UK'}, {'city': 'Paris', 'country': 'FR'}, {'city': 'Berlin', 'country': 'DE'}]
```

---

### Truthiness

🚫 Check if the list is empty/not empty:

```python
if len(data) == 0:
    print("List is empty")

if len(data) > 0:
    print("List is not empty")
```

✅

```python
if not data:
    print("List is empty")

if data:
    print("List is not empty")
```

---

### Flatten List of lists

```python
regular_list = [[1, 2, 3, 4], [5, 6, 7], [8, 9]]
flat_list = [item for sublist in regular_list for item in sublist]
print('Original list', regular_list)
>>> Original list [[1, 2, 3, 4], [5, 6, 7], [8, 9]]
print('Transformed list', flat_list)
>>> Transformed list [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

## Strings

---

A string can be seen as an **iterable** list of characters:

```python
data = 'oslo'
for letter in data:
    print(letter.upper())
>>> O
>>> S
>>> L
>>> O

data[2]
>>> 'l'
len(data)
>>> 4
data[::-1]
>>> 'olso'
[ord(x) for x in data]  # ord(x) == Unicode integer of character x
>>> [111, 115, 108, 111]
```

---

### Membership Check With `in`

🚫 Is substring in string:

```python
"restaurant".find("aura") > -1
>>> True
"waterfall".find("fun") > -1
>>> False
```

✅

```python
"aura" in "restaurant"
>>> True
"fun" in "waterfall"
>>> False
```

---

### Stripping Whitespace Characters

```python
data = '  empty spaces, what are we living for? '
print(data.strip())
>>> 'empty spaces, what are we living for?'
print(data.rstrip())
>>> '  empty spaces, what are we living for?'
print(data.lstrip())
>>> 'empty spaces, what are we living for? '
```

---

### Prefix/Suffix Manipulations

Added in Python 3.9:

```python
print("INFRA-123".removeprefix("INFRA-"))
>>> '123'
print("INFRA-123".removesuffix("-123"))
>>> 'INFRA'
```

---

### Tokenization

```python
string = 'lorem ipsum dolor sit amet'
tokens = string.split(" ")
tokens
>>> ['lorem', 'ipsum', 'dolor', 'sit', 'amet']
```

---

## Dicts

---

Dict is key-val storage:

```python
data = {'city': 'Berlin', 'country': 'DE', 'areas': ['Moabit', 'Mitte', 'Westend']}

data['areas'][1]
>>> 'Mitte'

data['city'] = 'Bielefeld'
data['city']
>>> 'Bielefeld'
```

---

### Iteration

Any dict is iterable:
```python
data = {'city': 'Berlin', 'country': 'DE', 'areas': ['Moabit', 'Mitte', 'Westend']}

# iterate other keys
for key in data:
    print(f"{key}: {data[key]}")
>>> city: Berlin
>>> country: DE
>>> areas: ['Moabit', 'Mitte', 'Westend']

# iterate over keys with values:
for key, val in data.items():
    print(f"{key}: {val}")
>>> city: Berlin
>>> country: DE
>>> areas: ['Moabit', 'Mitte', 'Westend']
```

---

### Membership Check With `in`

🚫

```python
data = {'city': 'Berlin', 'country': 'DE', 'areas': ['Moabit', 'Mitte', 'Westend']}
found = False
for key in data:
    if key == 'city':
        found = True
        break
found
>>> True
```

✅ 
```python
data = {'city': 'Berlin', 'country': 'DE', 'areas': ['Moabit', 'Mitte', 'Westend']}

'city' in data
>>> True
'population' in data
>>> False
'continent' not in data
>>> True
```

---

### Dict Comprehension

Formula: `{key: val for item in iterable}`

```python
data = {x: x.upper() for x in ['apple', 'banana']}
data
>>> {'apple': 'APPLE', 'banana': 'BANANA'}
```

---

### Accessing Values: `[]` vs. `get`

```python
data = {'a': 123, 'b': 456}
data['a']
>>> 123
data['b']
>>> 456
data['c']
>>> KeyError exception
```

---

```python
data = {'a': 123, 'b': 456}
data.get('a')
>>> 123
data.get('b')
>>> 456
data.get('c')
>>> None
data.get('c', 'default value')
>>> 'default value'
```

FYI, there's no `set` for dicts, values to be changes with the `[]` notation only (e.g. `data["key"] = "val"`)

---

### Safe Navigation

🚫 Error-prone code:

```python
data = {'a': {'b': {'c': 123}}}
element = data['a']['b']['c']
element
>>> 123

data = {'a': {'d': 456}}
element = data['a']['b']['c']
>>> Key Error!
```

✅ Robust way to inspect a dictionary:

```python
data = {'a': {'d': 456}}
element = data.get('a', {}).get('b', {}).get('c')
element
>>> None
```

---

### Merging 

```python
europe = {'Madrid': 'Spain', 'Rome': 'Italy'}
asia = {'Tokyo': 'Japan', 'Manila': 'Philippines'}
```

Before Python 3.9:

```python
{**europe, **asia}
>>> {'Madrid': 'Spain', 'Rome': 'Italy', 'Tokyo': 'Japan', 'Manila': 'Philippines'}
```

Starting Python 3.9:
```python
europe | asia
>>> {'Madrid': 'Spain', 'Rome': 'Italy', 'Tokyo': 'Japan', 'Manila': 'Philippines'}
```

---

## Tuples

---

Tuple is an **immutable**, **ordered** array of values:

```python
data = (1, 2, 3)
data[1]
>>> 2

data[1] = 10
>>> TypeError: 'tuple' object does not support item assignment
```

Tuples can be implicit:

```python
a = 1, 2
a[0]
>>> 1

# the same is:
a = (1, 2)
```

---

## Sets

---

Set is a **unordered** array of **unique** values:

```python
data = {1, 42, -1, 1}
>>> {1, 42, -1}

data[0]
>>> TypeError: 'set' object is not subscriptable
```

---

# 🧑‍🔧 Data Structures: Examples

---

## 🦄 Get Unique Elements of a List

Converting a list to a set removes duplicates:

```python
data = [5, 2, 3, 2, 4, 3, 1]
unique = list(set(data))
unique
>>> [1, 2, 3, 4, 5]
```

---

## 🔍 Search in a List of Objects

```python
data = [
    {"city": "Berlin", "country": "DE"},
    {"city": "Sydney", "country": "AU"},
    {"city": "Stockholm", "country": "SE"}
]

search = next((item for item in data if item["city"] == "Sydney"), None)
search["country"]
>>> 'AU'
search = next((item for item in data if item["city"] == "Paris"), None)
search is None
>>> True
```

---

## 🪡 Is Any of the Values

🚫

```python
if operation == "READ" or operation == "WRITE":
```

✅

```python
if operation in ["READ", "WRITE"]:
```

---

# 📦 Values Unpacking

---

## 🔁 Variable Swapping

🚫 Using a temporary variable:

```python
a = 5; b = 4
tmp = a
a = b
b = tmp
a
>>> 4
b
>>> 5
```

✅ Cut to the chase:

```python
a = 5; b = 4
a, b = b, a  # same as a, b = (b, a)
a
>>> 4
b
>>> 5
```

---

## 📭 Unpacking With Lists and Tuples

🚫

```python
data = ['one', 'two']
a = data[0]
b = data[1]
print(a)
>>> one
print(b)
>>> two
```

✅

```python
data = ['one', 'two']
a, b = data
a
>>> one
b
>>> two
```

---

Also works for tuples:

```python
data = ('one', 'two', 'many', 'things')
a, b, *c = data
c
>>> ['many', 'things']
```

```python
a, b = 123, 456  # same as a, b = (123, 456)
a
>>> 123
b
>>> 456
```

---

# 🌾 Data Classes

---

🚫 Describing objects can be done with dicts:

```python
d1 = {'name': 'Moabit', 'city': 'Berlin', 'country': 'DE', 'area': 7.72}
d2 = {'name': 'Greenwich', 'city': 'London', 'country': 'UK', 'area': 47.3}

d2['city']
>>> 'London'
```

Problem: no type hinting possible (e.g. that `name` is `str` and `area` should be a `float`) and there are no object structure restrictions in place.

---

🚫 We can use classes for solving it but that's bit too verbose:

```python
class District:
    def __init__(self, name: str, city: str, country: str, area: float):
      self.name: str = name
      self.city: str = city
      self.country: str = country
      self.area: str = area

d1 = District(name='Moabit', city='Berlin', country='DE', area=7.72)
d2 = District(name='Greenwich', city='London', country='UK', area=47.3)

d2.city
>>> 'London'
```

---

✅ Using data classes (added in Python 3.7):

```python
from dataclasses import dataclass

@dataclass
class District:
    name: str
    city: str
    country: str
    area: float = 0.0

d1 = District(name='Moabit', city='Berlin', country='DE', area=7.72)
d2 = District(name='Greenwich', city='London', country='UK', area=47.3)
d3 = District(name='Brooklyn', city='New York', country='US')

d2.city
>>> 'London'
d3.area
>>> 0.0
```

---

# 🦆 Type Hinting

There's no run-time type checking, but code with type hints allows:
- IDEs (e.g. [PyCharm](https://www.jetbrains.com/pycharm/)) and static type checkers (e.g. [mypy](http://www.mypy-lang.org/)) to catch errors before runtime
- to have a better, self-documented code

---

## Basic Type Hinting

🚫

```python
def sum_values(a, b):
    return a + b

sum_values(10, 3)
>>> 13
sum_values(10, "x")
>>> TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

✅

```python
def sum_values(a: int, b: int) -> int:
    return a + b

sum_values(10, "x")  # IDE will highlight an error
```

---

## Type Hinting & Multiple Types

Before Python 3.10:

```python
from typing import Union

def sum_values(a: Union[int, float], b: Union[int, float]) -> Union[int, float]:
    # a and b can be either int or float
    return a + b
```

Starting Python 3.10:
```python
def sum_values(a: int | float, b: int | float) -> int | float:
    return a + b
```

---

## Type Hinting & Containers

Before Python 3.10:

```python
from typing import Dict, List

def make_list(a: str, b: str) -> List[str]:
    # return type is a list of strings
    return [a, b]

def make_dict(k: str, v: str) -> Dict[str, str]:
    # return type is a dict with string keys and string values
    return {k: v}

make_list("hello", "world")
>>> ['hello', 'world']
make_dict("hello", "world")
>>> {'hello': 'world'}
```

Starting Python 3.10:
```python
def make_list(a: str, b: str) -> list[str]:
    return [a, b]

def make_dict(k: str, v: str) -> dict[str, str]:
    return {k: v}
```

---

## Type Hinting & Generic Objects

Before Python 3.10:

```python
from dataclasses import dataclass
from typing import List

@dataclass
class City:
  name: str
  country: str

def sort_cities(cities: List[City]) -> List[City]:
    return sorted(cities, key=lambda x: x.name)

cities = [
    City(name='Madrid', country='ES'),
    City(name='Berlin', country='DE'),
    City(name='Edinburgh', country='UK')
]

sort_cities(cities)
>>> [City(name='Berlin', country='DE'), City(name='Edinburgh', country='UK'), City(name='Madrid', country='ES')]
```

---

Starting Python 3.10:

```python
from dataclasses import dataclass

@dataclass
class City:
  name: str
  country: str

def sort_cities(cities: list[City]) -> list[City]:
    return sorted(cities, key=lambda x: x.name)
```

---

## Type Hinting and Local Variables

Not only limited to inputs/outputs of a function:

Before Python 3.10:

```python
from typing import List

result: List[str] = []  # not just a list of anything!
```

Starting Python 3.10:
```python
result: list[str] = []
```

---

# 👷‍♂️ Operators

---

## 👯‍♀️ Double Comparison

🚫

```python
if value > 0 and value < 100:
```

✅

```python
if 0 < value < 100:
```

---

## 🧬 Pattern Matching

Added in Python 3.10. Similar to `switch` statements in other languages, on steroids:

```python
def parse_command(command: str) -> str:
    match command.split():
        case [action, direction]:
            return f"Parsed: {action=}, {direction=}"
        case ["help"]: 
            return "Help message goes here"
        case _:
            return "Wrong command, 2 words expected"

parse_command("go north")
>>> "Parsed: action='go', direction='north'"
parse_command("look up")
>>> "Parsed: action='look', direction='up'"
parse_command("go")
>>> "Wrong command, 2 words expected"
parse_command("help")
>>> "Help message goes here"
```

---

Alias matching with `as`, `OR` matching with `|` and conditional matching:

```python
def parse_command(command: str) -> str:
    match command.split():
        case ["go", ("north" | "south") as direction]:
            return f"Going {direction}"
        case ["go", _]: 
            return "Sorry, can't go there!"
        case (["pick", obj, "up"] | ["pick", "up", obj]) if obj in ['shovel', 'rock']:
            return f"Picking up {obj}"
        case ["pick", _, "up"] | ["pick", "up", _]:
            return "Sorry, can't pick this up!"      
        case _:
            return "Wrong command, 2 words expected"

parse_command("go south")
>>> "Going south"
parse_command("go left")
>>> "Sorry, can't go there!"
parse_command("pick shovel up")
>>> "Picking up shovel"
parse_command("pick phone up")
>>> "Sorry, can't pick this up!"
```

---

Adapting to different structure types:

```python
from dataclasses import dataclass
from datetime import datetime

@dataclass
class User:
    age: int

def get_age(user: dict | User) -> int:
    match user:
        case User(age):
            return age
        case {"dob": {"age": int(age) | float(age)}}:
            return int(age)
        case {"dob": dob}:
            now = datetime.now()
            dob_date = datetime.strptime(dob, "%Y-%m-%d %H:%M:%S")
            return now.year - dob_date.year
```

```python
get_age({"dob": "1966-04-17 11:57:01"})
>>> 56
get_age({"dob": {"date": "1957-05-20T08:36:09.083Z", "age": 64}})
>>> 64
get_age({"dob": {"age": 39.6}})
>>> 39
get_age(User(age=40))
>>> 40
```

---

## 🍴 Ternary Operator

```python
if a == 5:
    result = "Five!"
else:
    result = "Not five..."
```

Shorter way to write the same:

```python
result = "Five!" if a == 5 else "Not five..."
```

---

## 🦷 Walrus Operator `:=`

Added in Python 3.8:

```python
value = 123
print(value)
>>> 123

# can be written as:
print(value := 123)
>>> 123
value
>>> 123
```

---

😒 Can be fine, but not the most concise way:

```python
numbers = [2, 8, 0, 1, 1, 9, 7, 7]

# get some stats on the list: length, sum, mean values

num_length = len(numbers)
num_sum = sum(numbers)

stats = {
  "length": num_length,
  "sum": num_sum,
  "mean": num_sum / num_length
}
>>> stats
{'length': 8, 'sum': 35, 'mean': 4.375}
```

✅ Doing the same with less lines of code:

```python
numbers = [2, 8, 0, 1, 1, 9, 7, 7]
stats = {
    "length": (num_length := len(numbers)), 
    "sum": (num_sum := sum(numbers)), 
    "mean": num_sum / num_length
}
>>> stats
{'length': 8, 'sum': 35, 'mean': 4.375}
```

---

## 🛂 `==` vs `is`

 - `==`: do two objects have the same contents?
 - `is`: are two objects the same thing (point to the same address in memory)?

```python
a = [1, 2, 3]
b = [1, 2, 3]

a == b
>>> True
```

```python
id(a)  # Python id of object a
>>> 4435362944
id(b)  # Python id of object b
>>> 4435377344 

a is b  # same as id(a) == id(b)
>>> False

a = b
a is b
>>> True
```

---

ℹ️ As a consequence:

```python
a = [1, 2, 3]
b = [1, 2, 3]
a[0] = 4
print(a, b)
>>> [4, 2, 3] [1, 2, 3]

a = b  # make a point to the same object as b, not copying contents of b!
a[0] = 4  # also changes b now as a and b point to the same address in memory
print(a, b)
>>> [4, 2, 3] [4, 2, 3]
```

---

### Copying an Object

🚫 Looks cryptic, and only works for lists but not for e.g. dicts:
```python
a = [1, 2, 3]
b = a[:]
a == b
>>> True
a is b
>>> False
```

✅

```python
a = [1, 2, 3]
b = a.copy()
a == b
>>> True
a is b
>>> False
```

---

ℹ️ There's only one global None object

```python
c = None
d = None

c == d
>>> True

c is d  # c and d and not "copies" of None, they point to it
>>> True
```

---

# 🧮 Named Parameters

```python
def print_issue_info(issue_id: str, issue_title: str)
    print(f"Issue id: {issue_id}, title: {issue_title}")
```

😒 Can be fine:

```python
print_issue_info("1234", "Create new thing")
>>> "Issue id: 1234, title: Create new thing"
```

✅ More explicit and human-readable:

```python
print_issue_info(issue_id="1234", issue_title="Create new thing")
>>> "Issue id: 1234, title: Create new thing"
print_issue_info(issue_title="Create new thing", issue_id="1234")
>>> "Issue id: 1234, title: Create new thing"
```

---

# 🏀 Practical Examples

---

## 📁 Reading/Writing Files

🚫 Handle errors yourself:

```python
f = open('data.txt', 'w')
try:
    f.write('hello, world')
finally:
    f.close()
```

✅ Use a [context manager](https://realpython.com/python-with-statement/) `with`:

```python
with open("data.txt", "r") as f:
    data = f.read()

with open("data2.txt", "w") as f:
    f.write(data)
```

---

## 🅾️ Loading/Exporting JSON

`json` is a built-in Python module:

```python
import json

data = {"a": 123, "b": None}
data_json = json.dumps(data)         # dumps = dump string
print(data_json)
>>> {"a": 123, "b": null}

data_parsed = json.loads(data_json)  # loads = load string
print(data_parsed == data)
>>> True
```

---

### Reading JSON Files

```shell
$ cat file.json
{
    "a": {"b": 123}
}
```

```python
import json

data = json.load(open("file.json"))  # data will be a dict
print(data["a"]["b"])
>>> 123
```

---

## 🌍 HTTP Requests

✅ Use the [requests](https://requests.readthedocs.io/en/latest/user/quickstart/) library:

```python
import requests

url = 'https://api.github.com/some/endpoint'
headers = {'Authentication': 'Bearer mytoken'}

r = requests.get(url, headers=headers)
print(r.status_code)
>>> 200
print(r.json())
>>> {"status": "OK", "message": "hi from the API"}
```

---

# 🔨 Tools

---

## 🔁 REPL

REPL = read-eval-print loop

Can be used to quickly try things out in a terminal:

```shell
$ python3
Python 3.10.6 (main, Aug 11 2022, 13:49:25) [Clang 13.1.6 (clang-1316.0.21.2.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> sum(range(0, 10))
45
```

---

## 🐞 Debugging

`breakpoint()` stops execution of the program at the given line and runs an interactive debugger (added in Python 3.7):

```python
value = 123
breakpoint()
(Pdb) value
>>> 123
```

---

# 🏁 Outro: Key Advice

- Write as short and lean code as possible
- Use the most recent version of Python
- Try ideas with REPL quickly
- Use type hinting
- Know your basic data structures
- Use list & dict comprehensions
- Use f-strings
- Use data classes
- RealPython.com is a great source of guide on specific topics ([example](https://realpython.com/python-type-checking/))

---

# 🙇‍♂️ Thank You!
