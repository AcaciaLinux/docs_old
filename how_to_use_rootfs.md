# AcaciaDevelopmentRootFS - RootFS

How to use:

- Create UEFI Virtual machine
- Select CPU-Type: host, since JS engine is compiled with host specific optimizations
- vdisk needs to be SATA, since this build has no initramfs for virtio-scsi drivers
- nic needs to be emulated Intel E1000, others might work..
- Partition disk with 1 fat32 EFI Partition and 1 ext4 Partition, (Optional: swap)
- Deploy tar.xz to empty ext4 partition (btrfs will work, but not with this kernel)
    mount ext4 partition and extract tar archive
    tar -xpf <location>/<name>.tar.xz
- refer to docs/how-to-install-grub.txt

Should boot?

# Tweaks

## grub-mkconfig from /etc/default/grub

In the stock image the grub bootloader configuration is written manually, we can generate it using grub-mkconfig, so you don't have to mess around with PARTUUIDs and that stuff.

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
linux	${rel_dirname}/${basename} root=${linux_root_device_thisversion} ro ${args}
```

to

```bash
linux	${rel_dirname}/${basename} root=${linux_root_device_thisversion} rw ${args}
```

take note that we changed "ro" to "rw", so linux allows to write to the root drive.

#### Generating the file

Now we can generate our grub.cfg file using the following command:

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```
