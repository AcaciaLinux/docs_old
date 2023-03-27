# Installing the AcaciaLinux base system

Once you have [set up](/installation/disk_setup.md) your disks and [mounted](/installation/mounting.md) them, you can start to install your new AcaciaLinux system.

> # **Warning**
>
> Make sure you have your leaf `root` configured correctly! If you execute these commands with leaf pointed to your root (`/`), it will most likely blow your current install into pieces!
>
> ### You have been warned!

> ### **Note**
>
> For these `leaf` commands to work, you *NEED* to be `root` and you have to be able to chroot, because the installation process leads leaf to chrooting into the new system for installing some packages.

## The system root
If you want to copy-paste all of these commands, it is important to set the environment variable `ACACIA_ROOT` correctly.
#### Example:
If you have your root partition mounted on `/mnt/`, you can export that using the following shell command:
```bash
export ACACIA_ROOT=/mnt/
```

## The leaf `root`
Leaf has the ability to redirect all of its actions to another root and the installation takes advantage of that. You will see every command with the prefix `--root $ACACIA_ROOT`. This instructs leaf to choose another root for operation.

## Updating
The first step to creating a new installation is to download the newest package lists from the mirror. You can do this by executing the following command:
```bash
leaf --root $ACACIA_ROOT update
```
There are some questions being asked about the permission to create new directories in your new root. This is a chance to check that `leaf` wants to create the directories in your new root and not `/`, which would most likely blow up your currently running install in the next step. You have been warned!

## Installing the core system
Now, let's install the most basic AcaciaLinux system by executing the following command:
```bash
leaf --root $ACACIA_ROOT install base bash leaf
```
This is the minimal set of packages required to install AcaciaLinux. You could omit the `leaf` package if you do not intend to install anything more from inside your new install, but are you really sure about that?

This environment gives you a `bash` shell and the `leaf` package manager to install any further tooling and packages.

> ### **Note**
>
> This system is nowhere near being bootable! There is no kernel and not even an init (except you want to use `bash` as your init).

## Continuing the installation
Now you can move on to [chrooting](/installation/chrooting.md) into your new system and [installing more packages](/installation/bootable_system.md).
