---
title: "Linux Kernel Topics"
weight: 12
---

## Linux kernel under GoboLinux

The Linux kernel differs from standard packages. It has nothing to be linked
against the legacy tree: no libraries, no binaries, no headers, no manuals or
info pages. Moreover, there are many things on a regular system which are very
tied to the kernel itself, such as the proc and sys filesystems, the device
nodes and the boot loader files.

These characteristics led to the creation of a special directory for the kernel,
called `/System/Kernel`. This tree is organized in the following way:

-   `/System/Kernel/Boot` - Bootloader files, including the kernel image
-   `/System/Kernel/Devices` - Device nodes, populated by Udev + Hotplug
-   `/System/Kernel/Modules` - Kernel modules
-   `/System/Kernel/Objects` - Sysfs, providing information gathered from Linux
    2.6
-   `/System/Kernel/Status` - The mounted proc filesystem

## Installing a kernel

Thanks to Compile, installing a new kernel is pretty straightforward on
GoboLinux. The Linux recipe takes into account the existence of a file called
config.gz inside `/System/Kernel/Status`. This file contains the current
configuration for the running kernel, and is used thereby to feed the new kernel
options.

In short, running **Compile Linux** will fetch the latest available recipe
(which already contains GoboLinux optional patches). After doing that, the
kernel itself is automatically downloaded, patched and filled with the current
configuration, taken from config.gz.

The menuconfig entry then appears, and allows for the user to modify their
kernel options. Just selecting "Exit" and telling the script to save the changes
will finish the user's interaction with the Linux kernel compilation. After
completed, a new entry will appear under
`/System/Kernel/Modules/$KERNEL_RELEASE`, and the new bzImage and System.map
files will get installed under /System/Kernel/Boot.

The old bzImage and System.map files aren't overwritten, though. They're just
symlinks to the current kernel image, and this guarantees that if something goes
wrong, a rollback can be done by simply modifying the kernel image at the GRUB's
bootloader prompt, and later by reverting the symlink's target to the previous
release.

To install a kernel which is newer than the available recipe, or one other than
vanilla, you may use NewVersion.

-   Download a kernel from [kernel.org](http://www.kernel.org/)

If you already have a kernel downloaded, or have a special source package, you
may place it in /Data/Compile/Archives.

-   Use
    `NewVersion Linux <Version> http://kernel.org/pub/linux/kernel/v2.6/<your-archive-name>`
    to create a recipe. Using a fake URL is all right if you don't intend to
    distribute the recipe.
-   Place any custom patches you need to apply into the
    `/Data/Compile/LocalRecipes/Linux/<Version>` directory.
-   Then Compile as usual.

## Kernel patches

The Linux recipe comes with a few patches in order to improve the user's
experience with the system. The patchset includes, but is not restricted to, the
following modifications:

-   [GoboHide]({{%relref "GoboHide" %}}): allows the legacy tree to be hidden from
    userspace applications
-   SquashFS: a compressed filesystem which gets uncompressed on demand. This
    filesystem is currently used on the GoboLinux ISO, and so it's interesting
    to have it in order to get the CD contents easily accessible through the
    _mount_ command
