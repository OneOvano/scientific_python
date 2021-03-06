 Make this file executable
 $ chmod +x strings.py
 Now you can start it just by name:
 $ ./strings.py
 Pay attention to write /usr/bin/env instead of a direct path to you python
 interpreter. This path can vary from system to system and when virtualenv is
 used.


 ```python 
from __future__ import division, print_function
 ``` 
 ## list

 ### "[]" operator

 Empty list

 ```python 
a = []
a = list()
 ``` 
 list is a collection of various elements that could be and could be not
 objects of the same type. List could be initialized using "[]" operator:

 ```python 
a = [1, 2.3, 4.3, -1 + 3.5j]
print(a)  # [1, 2.3, 4.3, -1+3.5j]
 ``` 
 Element access works as expected, index for the first element is zero, and
 for the last element is -1

 ```python 
print(a[0], a[-1], a[-2], a[-3], a[-4])

 ``` 
_1 (-1+3.5j) 4.3 2.3 1_ 


 ```python 
a[-1] = 12
print(a)  # [1, 2.3, 4.3, 12]
 ``` 
 ### Basic slicing

 Operator `[]` supports slicing. We will discuss slicing in more details later
 with `numpy` module.

 ```python 
b = a[1:-1]
print(b)  # [2.3, 4.3]
b = a[2:]
print(b)  # [4.3, 12]
b = a[1:2:]
print(b)  # [2.3]
b = a[::2]
print(b)  # [1, 4.3]
a[::2] = [-1, -4.3]
print(a)  # [-1, 2.3, -4.3, 12]
 ``` 
 ### Size of sequence

 Built-in function `len()` returns sequence size

 ```python 
print(len(a), len(b))  # 4 2
 ``` 
 ### Methods of the list and `del` statement

 list has some basic methods to manipulate with its data

 ```python 
print(a)  # [-1, 2.3, -4.3, 12]
 ``` 
 Add element

 ```python 
a.append(0)
print(a)  # [-1, 2.3, -4.3, 12, 0]
 ``` 
 Add object `-500` into the array with the index `1`. Negative indices also
 can be used

 ```python 
a.insert(1, -500)
print(a)  # [1, -500, 2.3, 4.3, 12, 0]
 ``` 
 Insert into on the penultimate index

 ```python 
a.insert(-1, 100)
print(a)  # [1, -500, 2.3, 4.3, 12, 100, 0]
 ``` 
 Remove and return the last element

 ```python 
x = a.pop()
print(x, a)  # 0 [-1, -500, 2.3, -4.3, 12, 100]
x = a.pop()
print(x, a)  # 100 [-1, -500, 2.3, -4.3, 12]
 ``` 
 Or any element by index

 ```python 
x = a.pop(1)
print(x, a)  # -500 [-1, 2.3, -4.3, 12]
 ``` 
 Also you can delete any object and in particular sequence element using `del`
 statement

 ```python 
del a[1]
print(a)  # [-1, -4.3, 12]
 ``` 
 Add all elements from another sequence (any iterabel object in general)

 ```python 
b = [1, 2, 3]
a.extend(b)
print(a)  # [-1, -4.3, 12, 1, 2, 3]
 ``` 
 .sort() performs in place and doesn't return anything

 ```python 
a.sort()
print(a)  # [-4.3, -1, 1, 2, 3, 12]
 ``` 
 ## For loop and `in` statement

 ### Basic example

 In Python for loop has a bit different syntax than in C-like languages. NB
 indention:

 ```python 
for x in [1, 2, 3, 4]:
    print(x)

 ``` 
_1_ 

_2_ 

_3_ 

_4_ 


 **Do not modify list while looping!**

 ### range()

 Looping works for any iterable variable. The special case of iterable object
 is a generator. A generator object doesn't hold all yielding values at once
 but calculate them on each lookup. The basic example of generator-like object
 is `range()` that yields a sequence of integers but doesn't hold them all in
 the memory. In Python 2 use xrange() instead of range().

 ```python 
for x in range(3):
    print(x)

 ``` 
_0_ 

_1_ 

_2_ 


 Another syntax:

 ```python 
for x in range(6, -1, -2):
    print(x)

 ``` 
_6_ 

_4_ 

_2_ 

_0_ 


 ### enumerate()

 Often we need to iterate both list elements and its indexes. Of course, you
 can iterate over index `for i in range(len(a))` and then get element by its
 index but more "pythonic" way is a usage of specific built-in function
 `enumerate()` for this purpose.


 ```python 
a = ['hello', 'world']
for i, x in enumerate(a):
    print(i, x)

 ``` 
_0 hello_ 

_1 world_ 


 ### `in`

 `in` statement has a stand-alone usage, it is an binary operator that returns
 `True` when the first variable is a member of the second variable.

 ```python 
a = [1, 2, 3, 4]
print(1 in a)  # True

try:
    a in 1
except TypeError as e:
    print(e)
 ``` 
 argument of type `int` is not iterable.

 Say hello exceptions, I wouldn't tell a lot about them, basically they work
 as in any other popular objective oriented languages like C++ or Java.


 ## Object model in Python

 ### Variables as references

 Most of the variables you will use in Python holds references to associated
 objects, not object themselves. The exceptions of this rule are some
 built-in objects like numbers.
 Let's show what does it mean practically:

 ```python 
a = [1, 2, 3]
b = a  # copy reference to the list, not list itself
a[0] = -1
print(a, b)  # [-1, 2, 3] [-1, 2, 3]
 ``` 
 But:

 ```python 
a = 1
b = a
a += 1
print(a, b)  # 2 1
 ``` 
 To copy list with its values use `.copy()` method (Python 3 only) or the
 module `copy` of the standard library

 ```python 
a = [1, 2, 3]
 ``` 
 We can use import in the any part of the code. Exception is `from __future__
 import ...`. The good style is importing all stuff at top of the file or
 function

 ```python 
import copy
b = copy.copy(a)  # or just a.copy() in Python 3
a[0] = -1
print(a, b)  # [-1, 2, 3] [1, 2, 3]
 ``` 
 More complex example:

 ```python 
a = [1, 2, 3, [4, 5, 6]]
b = copy.copy(a)  # In Python 3 you can use a.copy() instead
a[-1][0] = -100
print(a, b)  # [1, 2, 3, [-100, 5, 6]] [1, 2, 3, [-100, 5, 6]]
 ``` 
 What happens? copy.copy(a) is a shallow and copied only members of `a`, while
 its last member is a reference to another list that has been copied by
 reference not by values of its members. If you want copy to be deep
 (recursive) and copy all sub-members and sub-attributes of the object
 then you can use `copy.deepcopy()` function from `copy` module:

 ```python 
a = [1, 2, 3, [4, 5, 6]]
b = copy.deepcopy(a)
a[-1][0] = -100
print(a, b)  # [1, 2, 3, [-100, 5, 6]] [1, 2, 3, [4, 5, 6]]
 ``` 
 ### `is` statemnet

 `is` statement can be used to check if two variables hold references to the
 same object:

 ```python 
a = [1, 2, 3]
b = a
print(a is b)  # True
b = copy.copy(a)
print(a is b)  # False
 ``` 
 Let's compare `is` with equality operator `==`. `==` checks if all members
 of one object equals to the members of another object:

 ```python 
a = [1, 2, 3]
b = copy.copy(a)
print(a == b, a is b)  # True False
print([] == [], [] is [])  # True, False
print(True == 1, True is 1)  # True False
 ``` 
 Avoid using of `is` for basic types such numbers. It is highly implementation
 dependent and can cause unexpected results:

 ```python 
a = 511
print(511 is 511, a is 511, -100 is -100)  # True False False
 ``` 
 ### `None`

 `None` is a special built-in object. It is used when you need to return an
 "empty" value from the function or to send it as a function argument.
 Usually `None` is used as default value of an optional argument of a function
 (see, e.g. `dict.get()` bellow). It is an only object of NoneType, its
 Boolean value is `False` and every variable that holds None refers to this
 object. If a function doesn't have `return` statement or nothing is written
 after `return` then it returns `None`. You can check that your variable is
 None in several ways, but `is` and `is not` statements are recommended (see
 PEP 8, <http://pep8.org/#programming-recommendations>).

 ```python 
none = None
print(none is None)  # Recommended

 ``` 
_True_ 


 ```python 
a = 'hello'
print(a is not None)  # Recommended

 ``` 
_True_ 


    # print(none == None)  # Not recommended
_True_ 



 ## `tuple`

 ### Basics

 Empty tuple

 ```python 
t = ()
t = tuple()

t = (1, 2, 10 + 3j, 1, 'hello')
print(t.count(1))  # 2
print(t.index(1))  # 0
 ``` 
 Elements of a tuple can be accessed just like list's elements:

 ```python 
print(t[0])  # 1
print(t[-1])  # 'hello'
 ``` 
 ### One element tuple

 Be very careful when produce one element tuples. This is NOT a tuple:

 ```python 
a = (1)
print(a, type(a))  # 1 <class 'int'>
 ``` 
 But this _is_ a tuple:

 ```python 
a = (1,)
print(a, type(a))  # (1,) <class 'tuple'>
 ``` 
 I strongly recommend to use trailing comma in every place you are afraid to
 make a mistake like this. In the modern Python trailing comma is valid in
 almost every place you may want to use it.

 ### Mutability

 Tuples are immutable objects. That means that you cannot change their size,
 replace or add elements. NB that even operator "+=" will produce new object,
 not update current:

 ```python 
t = (1, 2, 10 + 3j, 1, 'hello')
tt = t
t += (-10, 'world')
print(t)  # (1, 2, (10+3j), 'hello', -10, 'world')
print(tt)  # (1, 2, (10+3j), 'hello')

try:
    t[0] = -1
except TypeError as e:
    print(e)

 ``` 
_tuple object does not support item assignment_ 


 Of course you still can modify mutable elements of the tuple:

 ```python 
t = (1, [2, 3])
t[1][0] = -100
print(t)  # (1, [-100, 3])
 ``` 
 ### Unpack values


 ```python 
t = (1, 2, 3)
a, b, c = t
print(a, b)  # 1 2
a, b = b, a
print(a, b)  # 2 1
 ``` 
 Use `_` variable to skip one of the values:

 ```python 
a, _, b = t
print(a, b)  # 1 3
 ``` 
 Variable `_` is a normal Python variable name, but usually this variable is
 used for such utility purposes.

 ### Return numerical values from functions

 Going ahead let me say that returning numerical values from the function will
 produce a tuple:



 ```python 
def f():
    return 1, 2


x = f()
print(x, type(x))  # (1, 2) <class 'tuple'>
a, b = f()
print(b, a)  # 2 1
 ``` 
 ## `dict` – dictionary

 `dict` is a hash-table dictionary type. That means that element access,
 insert and delete are all take $O(1)$ time

 ### Construction

 Empty `dict`

 ```python 
d = {}
d = dict()

d = {0: 'zero', 2: 'two', 10: 'ten'}
print(d)
 ``` 
 ### Value access

 Value access syntax is the same as for lists:

 ```python 
print(d[0])  # zero
d[12] = 'twelve'
print(12 in d)  # True
 ``` 
 Access to absent key produces exception

 ```python 
try:
    print(d[500])
except KeyError as e:
    print("Key doesn't exist:", e)

 ``` 
_Key doesn't exist: 500_ 


 Instead you can use `.get()` with the second optional argument that holds
 default return value:

 ```python 
print(d.get(500, 'Unknown value'))  # Unknown value
 ``` 
 `.get()` without the second argument will return `None`, i.e. the default
 value of the second argument of `.get()` is `None`

 ```python 
print(d.get(500))  # None
 ``` 
 ### Other methods

 Remove and return value by key:

 ```python 
print(d.pop(0))  # zero
 ``` 
 `del` statement works as usual:

 ```python 
del d[10]
 ``` 
 Add content from another dictionary, it replaces existing keys with new
 values:

 ```python 
d = {0: 'zero', 1: 'one'}
dd = {1: 'ONE', 2: 'TWO'}
d.update(dd)
print(d)  # {0: 'zero', 1: 'ONE', 2: 'TWO'}
 ``` 
 ### Hashable variables

 Note that not any object can be a key of a `dict`, but only a hashable
 object. A hashable object must have specific `.__hash__()` method that
 returns integral number, and such an object can be used as an argument of
 built-in `hash()` function. In general, all immutable objects are hashable.
 So you can use number types, `str` and `tuple` (without unhashable elements)
 as keys and cannot use `list` or `dict`.


 ```python 
d = {}
d[3 + 0j] = 'complex'
d[(1, 2, 3)] = 'tuple'
d['hello world'] = 'str'
try:
    d[[1, 2, 3]] = 'list'
except TypeError as e:
    print(e)

 ``` 
_unhashable type: 'list'_ 


 ### Iterating


 ```python 
d = {0: 'zero', 2: 'two', 10: 'ten'}
 ``` 
 Iteration over dictionary yields its keys in `random` (implementation-
 specific) order. (Note that since Python 3.7, specification says that `dict`
 returns values in the insertion order.) This equivalent to `for k in
 d.keys():`.

 ```python 
for k in d:
    print(k)

 ``` 
_0_ 

_2_ 

_10_ 

 The order can differ in Python 3.6 and earlier

 `in` statement will also look at keys, not values:

 ```python 
print(0 in d)  # True
print('zero' in d)  # False
 ``` 
 You can iterate over values of a dictionary using `.values()`. In Python 2
 use `.itervalues()` instead.

 ```python 
for v in d.values():
    print(v)

 ``` 
_zero_ 

_two_ 

_ten_ 

 The order can differ in Python 3.6 and earlier

 Also you can iterate over key-value pairs using `.items()`. In Python 2 use
 `.iteritems()` instead.

 ```python 
for k, v in d.items():
    print(k, v)

 ``` 
_0 zero_ 

_2 two_ 

_10 ten_ 

 The order can differ in Python 3.6 and earlier


 ## `set` and `frozenset`

 I have a _very good_ definition for this type: `set` is a hash-set.
 You can think that set is a dictionary without values: it can fast $O(1)$
 check if the element presents, you can add and delete elements from it.
 As a dictionary set is unordered, it means that iteration and popping
 elements orders are implementation specific. `set` can hold only hashable
 elements.

 An empty set

 ```python 
s = set()

s = {1, }  # This is a set, not dict. Trailing comma is optional.
s.add(1)
s.add(30)
print(s)  # {1, 30}

print(s.pop(), s.pop())  # 30 1
 ``` 
 Order can differ


 ```python 
s = set(range(5))
s.discard(3)
s.discard(10)  # Does nothing
print(s)

ss = {-1, -2}
s.update(ss)
print(s)  # {-1, -2, 0, 1, 2, 4}
 ``` 
 ### `frozenset`

 `frozenset` is an immutable variant of `set`.


 ```python 
fs = frozenset(range(5))
s = {}
s[fs] = 'frozenset'
print(s)  # {frozenset({0, 1, 2, 3, 4}): 'frozenset'}
 ``` 
 ## Examples

 I try to keep examples clean, so they can be unoptimized and slow

 ### Sorted list without duplicates


 ```python 
a = [1, 0, 0, -1, 1, 0, 3, 1, 0, 5, 2]
b = sorted(set(a))
print(b)  # [-1, 0, 1, 2, 3, 5]
 ``` 
 ### Count the most frequent element


 ```python 
d = {}
max_a_item = a[0]
for x in a:
    d[x] = d.get(x, 0) + 1
    if d[x] > d[max_a_item]:
        max_a_item = x
print(max_a_item)  # 0 
 ``` 
