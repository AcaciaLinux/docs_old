# Hosted install

A hosted install assumes a host Linux system that is able to build `leaf` and create the new AcaciaLinux system.

For this to work, you will need `root` access (or at least superuser rights) because you will manipulate filesystems and mount them into your existing system.

### 0. Before we start
The AcaciaLinux system gets installed into a mounted directory. We will be referring to this directory with the variable `$ACACIA_ROOT`. This can be any directory you want, but choosing one with less typework is beneficial (like `/mnt`).

### 1. Building leaf
Before you can start, you will need to clone the [leaf](https://github.com/AcaciaLinux/leaf) repository and build the package manager ([A guide on building leaf](/leaf/building.md)). You do not need to install it. Once you have access to the `leaf` binary, you can proceed.

### 2. Creating and mounting filesystems
After having access to `leaf`, you can start by creating and mounting your filesystems using [this guide](/installation/disk_setup.md). Once you have your root filesystem available, you can proceed to the next step.

### 3. Updating the package list
Once you have your filesystem available, you can instruct `leaf` to fetch the most up-to-date package lists:
```bash
leaf --root=$ACACIA_ROOT update
```
If you did not install `leaf` onto your host system, you can replace `leaf` with the path to your `leaf` binary.

There will be prompts that some directories are not existing (of course, we install a new system...), just answer with `Y`, `leaf` will do the rest.

### 4. Install the core system
Once `leaf` has its package lists available, it is fully functional and can install a system. To accomplish that, issue the following command to install the most basic system:
```bash
leaf --root=$ACACIA_ROOT install base bash leaf
```
After another question if you want to proceed, `leaf` installs the core AcaciaLinux system and itself, so you can continue building your system.
