# Python
#### Iterate through a dictionary

```
d = {'site1': {'servername': 'test.org', 'serveralias': 'www.test.org'}}

for key, value in d.iteritems():
    print key
    print value['servername']
```
