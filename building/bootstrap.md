# Bootstrapping a AcaciaLinux system

AcaciaLinux, using its packaging system `branch` and its package manager `leaf` can be bootstrapped quite easily, following these steps:

- Building a cross compiler toolchain
- Creating a package from the cross compiler toolchain
- Building some basic packages using the cross compiler toolchain
- Rebuilding the basic packages in release mode

## Prerequisites

Before starting to build a new `AcaciaLinux` system, make sure you have an existing Linux installation that is able to install `leaf` and `branch`. It should be able to use the `chroot` command and have some basic tools, such as `git`, `cmake`, `make`... installed.

> **Note**
> 
> This system should be powerful and have quite some available disk space (50GB should do just nice) and some RAM (8GB should do) in order to make this process not take forever. You will build `gcc`, `glibc` and some other large packages 4 times in total, you have been warned.

## Building a cross compiler toolchain

This is the first step in creating your own `AcaciaLinux` fork or instance. This toolchain gets build to completely abstract the new system from your existing build system. Using the [cross-toolchain](https://github.com/AcaciaLinux/cross-toolchain) repository, this shouldn't be too hard. Once you have your `tar` archive of the cross compiler root filesystem, you can upload it and proceed to step 2.

## Creating a package from the cross compiler toolchain

The previously built cross compiler toolchain now needs to get packaged into a `leaf` package, so it can be installed by `branch` to build the rest of the new system.

## Building some basic packages using the cross compiler toolchain

Referring to the file `cross_packages.txt` in the [BranchPackageBuilds](https://github.com/AcaciaLinux/BranchPackageBuilds) repository, you can see a list of packages that need to get compiled using the `cross` method in `branch`. This can be accomplished by using the command `branchclient -cb <package name>` for every package in this list. This basically rebuilds the previously cross compiled packages into `leaf` packages for later use. This is so the next packages can be build using the `release` method in `branch`. From these packages you should be able to rebuild these in the next step and then advance by building all the other packages you may need later on.

## Rebuilding the basic packages in release mode

Once you built some basic packages in `cross` mode and the resulting toolchain is able to build other packages, you can rebuild these packages to make sure they don't depend on any pieces of the cross toolchain. To accomplish this, you need to bump the `relaversion` in every packagebuild and submit it for building using the following command: `branchclient -rb <package name>`.

> **Warning**
> 
> Make sure you bumped the `realversion` before this step, else the new tools do not get used to compile other things, unless the `realroot` gets completely reinstalled.

## Finishing

Once you have completed these steps, you can start building all of your needed packages on top of these basic packages.
