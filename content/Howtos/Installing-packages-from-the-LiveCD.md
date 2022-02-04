---
title: "Installing packages from the LiveCD"
---

After installing GoboLinux and booting from the hard disk, you may want
to choose software packages from the Live CD to install. To do so, you
must mount the 'squashfs' file that contains the image from the Live CD
system.

To do that, first mount the CD then mount the desired GoboLinux squashfs
file:

    mount /Mount/CD-ROM
    mount /Mount/CD-ROM/GoboLinux-NonBase.squashfs /Mount/ SquashFS -t squashfs -o loop=/System/Kernel/Devices/loop0`

Now, you can use [InstallPackage](/Commands/InstallPackage) to install
software from the Program/ directory of the Live-CD:

    InstallPackage /Mount/SquashFS/Programs/Inkscape

Note 1: after using the squashfs file, you may want unmount it:

    umount /Mount/SquashFS

Note 2: To have the dependencies required by an application installed
automatically, use the `--batch` or `-b` parameter:

    InstallPackage --batch Gimp

-or-

    InstallPackage --batch /Mount/SquashFS/Programs/Gimp