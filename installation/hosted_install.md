# Hosted install

A hosted install assumes a host Linux system that is able to build `leaf` and create the new AcaciaLinux system.

For this to work, you will need `root` access (or at least superuser rights) because you will manipulate filesystems and mount them into your existing system.

### 0. Before we start
The AcaciaLinux system gets installed into a mounted directory. We will be referring to this directory with the variable `$ACACIA_ROOT`. This can be any directory you want, but choosing one with less typework is beneficial (like `/mnt`).

### 1. Building leaf
Before you can start, you will need to clone the [leaf](https://github.com/AcaciaLinux/leaf) repository and build the package manager ([A guide on building leaf](/leaf/building.md)). You do not need to install it. Once you have access to the `leaf` binary, you can proceed.

### 2. Creating and mounting filesystems
After having access to `leaf`, you can start by creating and mounting your filesystems using [this guide](/installation/disk_setup.md). Once you have your root filesystem available, you can proceed to the next step.

### 3. Installing the core system
You can now move on to the [next step, installing the core system.](/installation/core_system.md)
