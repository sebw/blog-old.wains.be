


date: 2007-07-18 17:23:07+00:00


# Lock MySQL table(s) in order to make a backup

categories:
- Linux
- SQL


In order to make a backup of a database, you have to make sure it's not modified while it is in the process of backup.

Let's see here how to lock a single table or a full database..

<!-- more -->

**Locking a table only :**

[root@host](1034)# mysql -p

mysql> CONNECT database;

# Locking..
mysql> LOCK TABLE table READ ;
Query OK, 0 rows affected (0.00 sec)

# This is the only way I have found to make sure the lock was active
mysql> INSERT INTO table VALUES ('1');
ERROR 1099: Table 'table' was locked with a READ lock and can't be updated

# Unlocking..
mysql> UNLOCK TABLES;
Query OK, 0 rows affected (0.00 sec)

# We make sure the lock is gone now..
mysql> INSERT INTO new VALUES ('1');
Query OK, 1 row affected (0.00 sec)

**Locking a whole database :**

[root@host](1034)# mysql -p

mysql> CONNECT database;

# Locking.. I term "flush" is inappropriate to my taste :)
mysql> FLUSH TABLES WITH READ LOCK ;
Query OK, 0 rows affected (0.00 sec)

# Checking the lock
mysql> INSERT INTO table VALUES ('1');
ERROR 1223 (HY000): Can't execute the query because you have a conflicting read lock

# Unlocking..
mysql> UNLOCK TABLES;
Query OK, 0 rows affected (0.00 sec)

# Lock is gone..
mysql> INSERT INTO table VALUES ('1');
Query OK, 1 row affected (0.00 sec)

**Locking from the bash prompt :**

I personnaly use this in a cron because I need to make a monthly backup of a huge database (around 16 Gb) that doesn't get a lot of changes. I use rsync to do that kind of backup (so making a backup of the .frm, .myi and .myd) and thus need to lock from the CLI or a script.

$ mysql -u login -p password -e "CONNECT database; LOCK TABLE table READ;"

You can create a file in the user directory to avoid passing the credentials at the CLI :

~/.my.cnf :

`[client]
user=user
pass=password`

**With mysqldump :**

mysqldump --add-drop-table --lock-all-tables --default-character-set=latin1 -uuser -ppassword DATABASE > dump.sql

The user always needs the lock rights.
