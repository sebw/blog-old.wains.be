# bash

#### integer increment

```
#!/bin/bash
	
x=1
echo $x
	
(( x++ ))
echo $x
	
(( x += 1 ))
echo $x
	
let x++
echo $x
```

### Take the date and insert it as metadata at the top of the file

Also, take the first line that starts with # and consider it as the title, add it as metadata, and remove it from the file.

Example filename: 2020-05-27-my-document.md

Example input:

```
# My document

Some text
```

Expected output:

```
---
date: 2020-05-27
title: My document
---

Some text
```

The script (it's ugly and piping one million sed is inefficient at best, but it works so..)

```
#!/bin/bash
for i in $(ls -1 2020-*); do
DATE=$(echo $i | awk -F'-' '{print $1 "-" $2 "-" $3}')
echo $DATE
TITLE=$(grep "^# " $i | head -n1 | sed 's/# //' | sed 's/:/-/g' | sed "s/'//g" | sed 's/"//g')
echo $TITLE

# insert the metadata
sed -i '1i---' $i
sed -i "2idate: $DATE" $i
sed -i "3ititle: $TITLE" $i
sed -i '4i---' $i

# remove the markdown title, now that it's in the metadata
sed -i '/^#\ /d' $i
done
```