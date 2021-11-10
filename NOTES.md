# Additional notes

## Bootloader update (optional)

You can use the Raspberry Pi [imager tool](https://www.raspberrypi.com/software/) to update the bootloader [docs](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#updating-the-bootloader).

Arch Linux ARM now has a package to update the bootloader of a running system (the same package that is used on Raspberry Pi OS).a

## Getting the SD Card(s) ready

TL;DR create two partitions, the first one is FAT32 LBA (type 0c) with 200M and the last one is Linux (type 83) filling the entire disk.

Linux commands:

All following commands must be executed as super user (ie. `sudo -i`).

```bash
lsblk # or blkid

find your sdcard

wipefs -a /dev/sdX # (optional) will erase all partitions on your sdcard

fdisk /dev/sdX # then follow the install instructions to create the partitions
```

Sample output:

```bash
fdisk -l /dev/sdb
Disk /dev/sdb: 59.52 GiB, 63908610048 bytes, 124821504 sectors
Disk model: MassStorageClass
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x1d0a82a3

Device     Boot  Start       End   Sectors  Size Id Type
/dev/sdb1         2048    411647    409600  200M  c W95 FAT32 (LBA)
/dev/sdb2       411648 124821503 124409856 59.3G 83 Linux
```


Disco /dev/mmcblk0: 14,46 GiB, 15523119104 bytes, 30318592 setores
