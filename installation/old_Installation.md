# AcaciaLinux Installation

The core installation package is currently not available. The package will soon be distributed as a tarball.

## The virtual machine

Currently it is recommended to test AcaciaLinux in a virtual machine. At the moment, we do not build a universal kernel, so the Kernel may not boot and we do not take any responsibility for any damage you may cause to your computer by testing this distribution.

### Qemu

Qemu provides a powerful emulator to test your OS in. AcaciaLinux currently requires:

- UEFI virtual machine

- Host-CPU

- Disk BUS needs to be **SATA**

- The NIC needs to be emulated Intel E1000, others might work

## Partitioning

From a running Linux system you will have to execute some commands.

You will need 2 partitions (3 if you wish to use a swap partition):

- EFI partition (FAT32 - 250Mb)

- root parition (ext4 - ...)

- [optional] swap partition (swap - ...)

You may now run the following commands as <u>root</u>:

### EFI partition

```bash
mksf.fat -F32 /dev/<your partition>
```

### root partition

```bash
mkfs.ext4 /dev/<your partition>
```

### swap partition (optional)

```bash
mkswap /dev/<your partition>
```

## Mounting

Once you have created your partitions, you will have to mount them as **<u>root</u>**. We recommend creating a mount-point as follows, the directory name can vary:

```bash
mkdir -p /mnt/acacialinux
```

Now you can mount your root partition, still as **<u>root</u>**:

```bash
mount /dev/<root partition> /mnt/acacialinux
```

## Deploying the root file system

Once you mounted your partitions, you may change your current working directory:

```bash
cd /mnt/acacialinux
```

And then download the root file system tarball (currently not available). Using the command ```ls``` you can determine the name of the tarball, say it is named ```acacialinux.tar.xz``` you can extract it using the following command (as **<u>root</u>**):

```bash
tar xpfv acacialinux.tar.xz
```

## Booting

You may now refer to [GRUB installation](https://github.com/AcaciaLinux/docs/wiki/GRUB) to make your AcaciaLinux bootable.