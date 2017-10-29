# awk oneliners

#### print every 20th line in the file data.txt

```
awk '(NR%20==0)' data.txt
```

- NF The number of fields in the current input record.
- NR The total number of input records seen so far.

#### print item in the last column of a list

```
echo "truc,machin,chose" | awk -F',' '{print $NF}'
```
