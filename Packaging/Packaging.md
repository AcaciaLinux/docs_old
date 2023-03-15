# Packaging
Packaging for [AcaciaLinux](https://github.com/AcaciaLinux) is made quite easy by the use of the packager [branch](https://github.com/AcaciaLinux/branch). You may install it using the `Makefile` in its git tree or by using the soon available [leaf](https://github.com/AcaciaLinux/leaf) package to continue with this guide.

## Initializing the package
Say, the package `myPackage` is to be packaged. It has version `1.22` and depends on the `base` package. To initialize the package, issue `branch init`. This will ask you some questions as listed:
```bash
>>> branch init
Initializing empty package directory.
Package name: 
myPackage
Package version: 
1.22
Package description: 
This is a sample package!
Package dependencies ([pkg1][pkg2][pkg3]): 
[base]
Package sdfg created.
```
## Adding files
You will find a new directory `myPackage-1.22`. Change into it using `cd myPackage-1.22` and you will see a file called `leaf.pkg` and a directory `data`. Now it is time to put your installed files into the `data` directory. If you have a package that supports `make DESTDIR=..... install`, change into the directory of the `Makefile` and target the data directory using the following command: 
```bash
make DESTDIR=/path/to/myPackage-1.22/data install
```
The `Makefile` will install all the needed files into the `data` directory, which is later deployed to the root of the installation by the `leaf` package manager.
## Finalizing the package
Once all your files are in the `data` directory, change into the package directory using
```bash
cd /path/to/myPackage
```
and issue the following command to let branch create the `.lfpkg` file:
```bash
branch pack
```
If you have set up `sftp` support for branch, you can let branch push and append the package immediately to the remote `leaf.pkglist` file using the following command:
```bash
branch packpush
```