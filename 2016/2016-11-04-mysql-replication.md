# MySQL 5.6 quick and dirty replication

```
Some assumptions:  
master> = mysql commands on master  
slave> = mysql commands on slave  
root@master = bash commands on master  
root@slave = bash commands on slave  
/var/lib/mysql/master01-bin.* = name of the replication logs, depending on your config
```

master> STOP MASTER
root@slave: service mysqld stop



```
```