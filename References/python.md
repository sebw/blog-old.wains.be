# Python

#### Print doc

```
import os

print(os.__doc__)
print(os.open.__doc__)
```

#### Validate code against pep8

```
$ sudo pip install pep8
$ pep8 mycode.py
```

#### Iterate through a dictionary

```
d = {'site1': {'servername': 'test.org', 'serveralias': 'www.test.org'}}

for key, value in d.iteritems():
    print key
    print value['servername']
```

#### Iterate through a list
```
l = {'un','deux'}

for value in l:
    print value
```

#### Transform a dict in list

```
d = {'key': 'value'} <-- d = dict
l = d.items() <-- l = list
```

Not to be confused with iteritems(), an iterator over the key and values of a dict.

#### args vs kwargs (keyword arguments)

```
def list_all_args(*args):    print argslist_all_args('truc','machin','chose')
```

args is returned as a tuple

```
def test(**kwargs):    for key, value in kwargs.items():        print key + '=' + valuetest(truc='val',machin='chose')
```

kwargs is returned as a dict