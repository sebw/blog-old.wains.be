# sed

#### Remove comments (#) from file

Input file looks like this

```
$ cat infile
# this is a comment
echo 'some stuff'
```
Run sed

```
$ sed '/^\#/d' infile > outfile
```
Output file

```
$ cat outfile
 this is a comment
echo 'some stuff'
```
