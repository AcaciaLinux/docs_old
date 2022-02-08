# Installing GRUB

Installing grub to a scratch linux system comes with some difficulties, an explanation can be found in this file.

## Mounting partitions

First of all, we have to mount the partitions and switch to a chroot, if you come from the installation and have not quit the chroot, you can skip this step.

```bash
export MOUNTPOINT=/path/to/your/mounted/root/partition
mount -v --bind /dev $MOUNTPOINT/dev
mount -v --bind /dev/pts $MOUNTPOINT/dev/pts
mount -t proc proc $MOUNTPOINT/proc
mount -t sysfs sysfs $MOUNTPOINT/sys
mount -t tmpfs tmpfs $MOUNTPOINT/run
```

Then mount the EFI parition:

```bash
mkdir -p $MOUNTPOINT/boot/efi
mount /dev/<your_efi_partition> $MOUNTPOINT/boot/efi
```

## Changing to chroot

Now, once all the partitions have been mounted, you can chroot into the new rootfs:

```bash
chroot $MOUNTPOINT /usr/bin/bash
source /etc/profile
```

The second command gets run in the chroot, so the current bash profile gets loaded

## Setting mountpoint and efivars

Once in the chroot, we can mount our efivars using the following command:

```bash
mountpoint /sys/firmware/efi/efivars || mount -v -t efivarfs efivarfs /sys/firmware/efi/efivars
```

## Installing GRUB

##### **Before proceeding, make sure you have mounted your EFI partition!**

GRUB can be installed using the following command:

```bash
grub-install --target=x86_64-efi --bootloader-id=<MYID> --efi-directory=</my/efi>
```

You have to replace the following placeholders:

- **MYID** Is your desired bootloader id, something like "Linux" or "AcaciaLinux" can be chosen, or something else, this is customization at the bootloader level

- **/my/efi** Is your efi directory, if you followed this guide, this should be **/boot/efi/**

Your installation is successful if the output is the following

```
Installing for x86_64-efi platform.
Installation finished. No error reported.
```

## Tweaking the filesystem

For now, it is necessary to tweak the filesystem so you can use grub-mkconfig to create your config. In the stock image the grub bootloader configuration is written manually, we can generate it using grub-mkconfig, so you don't have to mess around with PARTUUIDs and that stuff.

#### /etc/default/grub

First of all, create the following file: /etc/default/grub:

```shell
GRUB_DEFAULT=0
GRUB_TIMEOUT=1
GRUB_DISTRIBUTOR="AcaciaLinux"
GRUB_CMDLINE_LINUX_DEFAULT="loglevel=5"
GRUB_CMDLINE_LINUX=""
GRUB_DISABLE_OS_PROBER=false
GRUB_GFXMODE=1920x1080
GRUB_GFXPAYLOAD_LINUX=keep
GRUB_DISABLE_LINUX_UUID=true
GRUB_DISABLE_LINUX_PARTUUID=false
```

#### /etc/grub.d/10_linux

Next, we have to edit /etc/grub.d/10_linux,change the line around line 144:

```bash
linux    ${rel_dirname}/${basename} root=${linux_root_device_thisversion} ro ${args}
```

to

```bash
linux    ${rel_dirname}/${basename} root=${linux_root_device_thisversion} rw ${args}
```

Note that only "ro" was chaged to "rw " in this line, this is to tell linux to make the root partition writeable

#### Generating GRUB config file

Now we can generate our grub.cfg file using the following command:

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```


