


date: 2007-12-17 21:03:05+00:00


# 'BackupPC : "File::RsyncP module doesn''t exist"'

categories:
- Debian/Ubuntu
- Linux


If you are trying to get [BackupPC](http://backuppc.sourceforge.net) running under Debian and get the following message :

`File::RsyncP module doesn't exist`

Make sure you have the following package installed :

`apt-get install libfile-rsyncp-perl`
