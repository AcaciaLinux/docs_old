# Disk setup

All linux distributions need at least a `root` partition. It is recommended to have a `swap` partition and if you want to boot your system, you will need a `EFI` partition. If you desire, you can have a separate home partition.

To configure the partition layout, you may use a program such as `parted` or `cfdisk`. There is an ample amount of guides in the internet on how to use them.

## `root` [`*`]
```yml
size: As much as you want (At least ~5GB)
filesystem: ext4 / btrfs...
mountpoint: /
```
```bash
mkfs.<filesystem> <your partition>
```
```bash
mount <your partition> $ACACIA_ROOT/
```
The `root` partition is the most important and the largest one, it will contain all the files needed in the system. You can choose any filesystem you please, but it has to be supported by the AcaciaLinux kernel.


## `home` [`*`] (optional)
```yml
size: As much as you want (This is where the bulk of your files will go)
filesystem: ext4 / btrfs...
mountpoint: /home/
```
```bash
mkfs.<filesystem> <your partition>
```
```bash
mount <your partition> $ACACIA_ROOT/home/
```
If you desire to split your home partition from your system partition, you can create a separate home partition and mount it.

## `EFI` [`fat32`]
```yml
size: 256M
filesystem: fat32
mountpoint: /boot/efi/
```
```bash
mkfs.fat -F32 <your partition>
```
```bash
#You need to mount root first!
mkdir -p $ACACIA_ROOT/boot/efi/
mount <your partition> $ACACIA_ROOT/boot/efi/
```
The `EFI` partition contains the bootloader for the system. If you install AcaciaLinux and do not want to boot it using a bootloader you can omit this partition.

## `swap` [`swap`]
```yml
size: Typically like your RAM (can be larger if needed)
filesystem: swap
mountpoint: swap
```
```bash
mkswap <your partition>
```
```bash
swapon <your partition>
```
Finally the `swap` partition. It is optional but required if you want to configure your system for hibernate (suspend to disk).

# Example
A typical filesystem layout on a machine with `512GB` of storage and `8GB` of RAM may look as follows:
```yml
/dev/sda1: #EFI
    size: 1GB
    filesystem: fat32
    mount: /boot/efi/
    create_command: mkfs.fat -F32 /dev/sda1
    mount_command: mount /dev/sda1 /boot/efi/

/dev/sda2: #swap
    size: 8GB
    filesystem: swap
    mount: swap
    create_command: mkswap /dev/sda2
    mount_command: swapon /dev/sda2

/dev/sda3: #root
    size: 100GB
    filesystem: btrfs
    mount: /
    create_command: mkfs.btrfs -F32 /dev/sda3
    mount_command: mount /dev/sda3 /

/dev/sda4: #home
    size: 403GB
    filesystem: btrfs
    mount: /home/
    create_command: mkfs.btrfs /dev/sda4
    mount_command: mount /dev/sda4 /home/

```