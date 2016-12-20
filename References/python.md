# Python

#### Data types

```
List: ['value1', 'value2']  
Dict: {'key1':'value1', 'key2':'value2'}  
Set (unordered list):
    settest = set('This is a test')
    set(['a', ' ', 'e', 'i', 'h', 's', 'T', 't'])
Tuple (immutable list): ('value1', 'value2')  
```

#### Importing

```
from subprocess import call
call("ls", "-l")
```
```
import subprocess
subprocess.call("ls", "-l")
```

#### Print doc

```
import os

print(os.__doc__)
print(os.open.__doc__)
```

#### Validate code against PEP8

```
$ sudo pip install pep8
$ pep8 mycode.py
```

#### Iterate through a dictionary

```
d = {'site1': {'servername': 'test.org', 'serveralias': 'www.test.org'}}

for key, value in d.iteritems():
    print key + ": " + value['servername']
```

#### Check for a value in a list

```
>>> grains = ["role1","role2","role3"]
>>> "role2" in grains
True
```

#### Check for a value in a dict

``` 
>>> grains = {"roles": ["role1", "role2", "role3"]}
>>> "role2" in grains["roles"]
True
```

#### Iterate through a list or set
```
l = {'un','deux'}

for value in l:
    print value
```

#### Insert or append items to a list
```
l = ['one','three']
l.insert(1,'two')

insert() takes two args, first one is zero based position, second is the value

Result: ['one', 'two', 'three']

l.append('four')

Result: ['one', 'two', 'three', 'four'] 

```
#### Update a dict
```
d = {'one':1,'two':2}
d.update({'three':3})

Result: {'three': 3, 'two': 2, 'one': 1}
```

#### Transform a dict in list

```
d = {'key': 'value'}
type(d)
> dict

l = d.items()
type(l)
> list
```

Not to be confused with iteritems(), an iterator over the key and values of a dict.

#### Args vs. kwargs (arguments vs keyword arguments)

`*args` is a tuple  
`**kwargs` is a dict

##### args

```
def list_args(*args):    print argslist_args('truc','machin','chose')
```

Output:

```
('truc', 'machin', 'chose')
```

##### kwargs

```
def list_kwargs(**kwargs):    for key, value in kwargs.items():        print key + '=' + valuelist_kwargs(truc='val',machin='chose')
```

Output:

```
machin=chose
truc=val
```

**kwargs is a dict

##### Specified number of args

```
def list_args(first, second):
    print first + ', ' + second
    
list_args('Bonsoir', 'Elliot')
```

Output:

```
Bonsoir, Elliot
```

`list_args('Bonsoir')` would return a `list_args() takes exactly 2 arguments (1 given)`

#### Print a sequence of integers

range() returns a list

takes two args maximum.

```
>>> range(10)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> range(0,20)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19] [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
```

#### Printing unicode characters

```
print u'\u2713'
```

#### Simple regexp matching

```
import re

re_pattern = "^.*\ "

re_input = "this is a test"

for result in re.findall(re_pattern, re_input):
    print "Result --> ", result
```

Output:

```
Result --> this is a
```