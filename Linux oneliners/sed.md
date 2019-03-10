# sed

#### Remove comments from a file

Input file looks like this:

```
$ cat infile
# this is a comment
echo 'some stuff'
```

Run sed:

```
$ sed '/^\#/d' infile > outfile
```

Output file:

```
$ cat outfile
echo 'some stuff'
```
