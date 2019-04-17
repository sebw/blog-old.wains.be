# Remove Docker orphans volume with a script

```
for j in $(for i in $(docker volume ls -qf dangling=true)
do
docker volume inspect $i | grep "Mountpoint" | awk -F':' '{print $2}' | awk -F'"' '{print $2}'
done)
do
du -h --max-depth=1 $j
done
```