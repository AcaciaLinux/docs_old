# Installing a bootable system
Once you [chrooted](/installation/chrooting.md) into your new AcaciaLinux root, you can start off by installing a kernel and some core system components to make your system usable and bootable.

> # **Warning**
>
> Make sure you are in fact chrooted into your new system! If you aren't this could completely destroy your host system!
>
> ### You have been warned!

# Installing the packages:
In short, use the following command to install the most commonly needed utils:
```bash
leaf install linux-lts linux-firmware systemd grub dracut networkmanager vim
```
This will install some basic packages to make your system bootable and give you the chance to install further packages.

## Installed packages
This is an explanation of the just installed packages. If you really don't need a component, you can omit it, but read what it is needed for first!

#### linux-lts
The Linux kernel is needed for making a usable system. Note that currently we are still using the host kernel, but once we boot the newly installed system, we have to provide our own kernel.
#### linux-firmware
Some hardware needs firmware to work correctly... If you are installing AcaciaLinux in a virtual machine, you don't need this package.
#### systemd
Systemd is your init system, if you do not want to start your whole system manually by punching loads of commands into bash, you really want to install this.
#### grub
GRUB is the bootloader that allows our kernel to even start. There are some alternatives but GRUB is really versatile and common amongst other distros.
#### dracut
Dracut is an initramfs generation tool. The initramfs is needed for solving the classic chicken and egg problem where the kernel needs a driver for mounting the root partition but the driver is on the root partition.
#### networkmanager
This is a daemon that configures the network for you. You can omit this if you don't want to connect to the internet or really like configuring your NIC manually.
#### vim
An editor is quite handy...
