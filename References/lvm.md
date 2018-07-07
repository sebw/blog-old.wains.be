# LVM

PV = physical volume  
VG = volume group  
LV = logical volume  

LV's are inside VG's made of PV's, themselves made of LVM partitions.

LVM partitions don't need to be formatted in any way. That's the LV that will be formatted.

```
+------+------+------+
| LV01 | LV02 | LV03 |
+------+-------------+
|     volumegroup01    | volumegroup02 |
+------+-------------+
| PV01 | PV02 | PV03 |
+------+------+------+
| sdb1 | sdc1 | sdc2 |
+------+------+------+
```

#### Create LVM partitions:

- fdisk /dev/sdb
- create new partition /dev/sdb1
- change partition type to 8e (LVM)

#### Create PV:

`pvcreate /dev/sdb1`

#### Extend existing VG or create a new one:

`vgextend volumegroup01 /dev/sdb1`

or

`vgcreate volumegroup02 /dev/sdb1`

#### Create a new LV of 1GB inside existing VG and another LV using the rest of available space in the VG:

`lvcreate -L 1G -n logicalvolume03 volumegroup01`

`lvcreate -l 100%FREE -n logicalvolume04 volumegroup01`

#### Or resize an existing LV:

```
lvresize -L +5G --resizefs volumegroup01/logicalvolume02
resize2fs /dev/volumegroup01/logicalvolume02
```

#### Remove an active LV:

Make sure the LV doesn't contain an active mounted filesystem.

`lvremove /dev/volumegroup01/logicalvolume02`

#### Format and mount LV:

```
mkfs.xs /dev/volumegroup01/logicalvolume02
blkid
edit /etc/fstab
```