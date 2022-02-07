---
title: "Installing to external storage devices"
menuTitle: "External storage devices"
weight: 6
---

GoboLinux 016 comes with two installation modes: UEFI and BIOS-compatibility
mode. Depending on how your computer firmware is configured you may need to
follow one or another recipe below.

## BIOS-compatibility mode

Ensure that your external disk has been configured with a **MSDOS** partition
table. You need to have at least one Linux partition (e.g., ext4), with the
**BOOT flag** set.

You can then proceed with the installation of GoboLinux by selecting that Linux
partition as install target and by enabling the installation of the bootloader
on the master boot record (MBR) of that disk.

## UEFI mode

Ensure that your external disk has been configured with a **GPT** partition
table. You need to have at least one Linux partition (e.g., ext4) and a **FAT
(32/16/12)** partition which is where the UEFI application embedding the GRUB
bootloader will be stored. The FAT partition needs to have both the **ESP** and
**BOOT** flags set. If you are using GParted, that FAT partition will be
automatically formatted by the tool. If you are not, then make sure to invoke
`mkfs.msdos` to format it yourself.

Once the partitioning is arranged, you can proceed with the installation of Gobo
by selecting the Linux partition as system install target and by selecting the
FAT partition (also called _EFI System Partition_) as bootloader install target.

## Troubleshooting

### Unable to mount root fs

Both USB-Storage and UAS (USB-Attached-SCSI) drivers are built into the kernel.
However, at times the kernel may not have time to discover the partitions on
your external disk and may fail to mount the root filesystem. This particular
problem can be fixed by adding the `rootwait` parameter to the kernel command
line.

For BIOS-compatibility mode:

1. Mount your system partition using the LiveCD under `/Mount/GoboLinux`
2. Edit the file at `/Mount/GoboLinux/System/Kernel/Boot/grub/grub.cfg`. Look
   for the lines starting with `linux /System/Kernel/Boot/kernel-4.8.2-Gobo` and
   append the word `rootwait` to the very end of those lines
3. Unmount the partition under `/Mount/GoboLinux` and reboot.

For UEFI mode:

1. Mount your boot partition (the one with a FAT filesystem) using the LiveCD
   under `/Mount/GoboLinux`
2. Edit the file at `/Mount/GoboLinux/EFI/BOOT/grub-efi.cfg`. Look for the lines
   starting with `linux /System/Kernel/Boot/kernel-4.8.2-Gobo` and append the
   word `rootwait` to the very end of those lines
3. Regenerate the UEFI application. This is a large command, so it's better to
   just copy+paste it.

```fish
cd /Mount/GoboLinux/EFI/BOOT
grub-mkstandalone-efi -d /lib/grub/x86_64-efi -O x86_64-efi --modules="part_gpt part_msdos iso9660 all_video efi_gop efi_uga video_cirrus gfxterm gettext font" --fonts="unicode" --themes="" -o BOOTx64.EFI --compress=gz "boot/grub/grub.cfg=grub-efi.cfg"
```

Afterwards, unmount the partition under `/Mount/GoboLinux` and reboot.
