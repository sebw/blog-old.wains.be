# Luks

# Luks on a file

As root:

Create a 10MB empty file:

```
dd if=/dev/zero bs=1M count=10 of=encrypted-file
```

Format the file as a LUKS partition:

```
cryptsetup luksFormat encrypted-file
```

Answer "YES" and choose a strong password.

Open the file and give it a device name:

```
cryptsetup luksOpen encrypted-file encrypted-device
```

`fdisk -l`  should show a `/dev/mapper/encrypted-device` device.

Format it:

```
mkfs.xfs /dev/mapper/encrypted-device
```

Mount:

```
mkdir /mnt/luks
mount /dev/mapper/encrypted-device /mnt/luks
```

Unmount and close:

```
umount /mnt/luks
cryptsetup luksClose encrypted-device
```