


date: 2006-10-02 09:38:00+00:00


# Truecrypt on Ubuntu 6.06 kernel 2.6.15

categories:
- Howto
- Linux
- Security


# sudo su -

# apt-get install linux-source-2.6.15

# cd /usr/src

# tar –xvjf linux-source-2.6.15.tar.bz2

# ln –s linux-source-2.6.15 linux

# apt-get install build-essential gcc-3.4 

# export CC=gcc-3.4

# make -C /usr/src/linux-source-2.6.15 config modules

# tar -xvfz truecrypt-4.1-source-code.tar.gz

# cd truecrypt-4.1-source-code/Linux/

# ./build.sh

# ./install.sh

You're done !

