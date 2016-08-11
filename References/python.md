# Python

#### Data types

```
List: ['value1', 'value2']  
Dict: {'key1':'value1', 'key2':'value2'}  
Set: {'key1', 'key2'}
Tuple: ('value1', 'value2')  
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

#### Iterate through a list
```
l = {'un','deux'}

for value in l:
    print value
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

#### args vs kwargs (arguments vs keyword arguments)

*args is a tuple  
**kwargs is a dict

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