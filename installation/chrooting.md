# Chrooting
Once you have a basic AcaciaLinux in place, you can chroot into it by installing the `setup-scripts` package using leaf. If you are installing AcaciaLinux from the Live ISO, this has already been done for you.

## The system root
If you want to copy-paste all of these commands, it is important to set the environment variable `ACACIA_ROOT` correctly.
#### Example:
If you have your root partition mounted on `/mnt/`, you can export that using the following shell command:
```bash
export ACACIA_ROOT=/mnt/
```

# Copying `resolv.conf`
You need to copy the resolver config to your root, else `leaf` won't be able to contact the package server. To accomplish this, use the following command to copy the host `resolv.conf` into the guest:
```bash
cp /etc/resolv.conf $ACACIA_ROOT/etc/resolv.conf
```

# Chrooting
The chroot process is normally quite involved due to the need of mounting a couple of kernel filesystems into the guest, but the handy `acacia-chroot` script takes care of that (installed with the `setup-scripts` package):
```bash
acacia-chroot $ACACIA_ROOT
```
This should greet you in your new system with a shell. You can now continue to [install more packages to build out your system](/installation/bootable_system.md).
