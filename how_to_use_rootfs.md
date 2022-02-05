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
