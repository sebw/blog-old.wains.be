# Data recovery with Linux: useful tools
date: 2008-01-04 22:02:52+00:00

Tags: Linux, Security, Tools

Today, I had to recover some data from a (badly) failed drive. The drive was coming from a laptop. I first tried to recover stuff using the Ubuntu Live CD on the laptop, but it didn't work. Whenever I was trying to install the necessary tools in the Live CD environment, the system was hanging and throwing IO errors from the failed drive.

I attached the drive (using a 2"1/2 to 3"1/2 adapter) to my desktop machine and booted under Ubuntu.

It was impossible to mount the drive directly (returning IO errors immediately).

dd was not able to copy the content of the drive, because of the bad sectors.

## dd_rescue
The tool **dd_rescue** (from the package **ddrescue**) came to help.. It found errors at around 2.8 GB and 13 GB but kept going. I'm now in possession of a file that can be mounted and I can recover the precious files.

Usage :

`dd_rescue -l errors.log /dev/sdc1 /path/to/destination/diskdump`

Here's the description of ddrescue : copies data from one file or block device to another dd_rescue is a tool to help you to save data from crashed partition. It tries to read and if it fails, it will go on with the next sectors where tools like dd will fail. If the copying process is interrupted by the user it is possible to continue at any position later. It can copy backwards.

## gddrescue, dcfldd and rdd
These are apparently similar tools. I haven't tested them.

Searching for the word "forensic" in Synaptic returned some interesting tools.

## Foremost
Forensics application to recover data.  This is a console program to recover files based on their headers and footers for forensics purposes.

Foremost can work on disk image files, such as those generated by dd, Safeback, Encase, etc, or directly on a drive. The headers and footers are specified by a configuration file, so you can pick and choose which headers you want to look for.

Usage :

`foremost -t jpg -i diskdump`

This would recover jpg files from diskdump and copy the recovered files in the current directory

## Vinetto
A forensics tool to examine Thumbs.db files A tool intended for forensics examinations. It is a console program to extract thumbnail images and their metadata from those thumbs.db files generated under Windows. Used in forensic environments.

Usage :

`vinetto Thumbs.db -o /tmp/dir`

This would recover the cached preview images from Thumbs.db into /tmp/dir

## sleuthkit
Tools for forensics analysis The Sleuth Kit (previously known as TASK) is a collection of UNIX-based command line file system and media management forensic analysis tools. The file system tools allow you to examine file systems of a suspect computer in a non-intrusive fashion. Because the tools do not rely on the operating system to process the file systems, deleted and hidden content is shown.

You can use "autopsy" as front-end to sleuthkit.

## gdmap
Tool to visualize diskspace GdMap is a tool which allows to visualize disk space. Ever wondered why your hard disk is full or what directory and files take up most of the space? With GdMap these questions can be answered quickly. To display directory structures cushion treemaps are used which visualize a complete folder or even the whole hard drive with one picture.

The purpose here was to recover files from a failed drive.. not doing forensics, so only dd_rescue  was really needed today.

I'll try to keep a list of useful recovery/forensics tools in this post.

If you have suggestions about tools, technique, etc. drop me a line.
