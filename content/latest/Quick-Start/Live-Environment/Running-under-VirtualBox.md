---
title: "Running under VirtualBox"
linkTitle: "VirtualBox"
weight: 2
---

> [!NOTE] Note
> This article has been written for an older GoboLinux
> release, and is potentially out of date!!

### Setting up VirtualBox guest additions

VirtualBox requires its own graphics drivers in order to perform advanced
features such as smart mouse sharing and running at a window-dependent full
resolution.

These drivers can be built using the "Guest Additions" ISO image included with
VirtualBox.

The catch is that we are already using the virtual CD drive from VirtualBox to
run the ISO, so we need to add a second one. With the virtual machine shut down,
right-click the image, then at the Storage pane, add a second optical drive, and
insert the `VBoxGuestAdditions.iso` file that should be somewhere in your
VirtualBox installation:

![VirtualBox Settings - Storage](../images/virtualbox_storage.png)

Then, boot GoboLinux normally in VirtalBox, and do the following:

```fish
mount /dev/sr1 /Mount/CD-ROM
cd /Mount/CD-ROM
./VBoxLinuxAdditions.run
udevadm trigger
```

When you run `udevadm trigger` the drivers should be loaded, and the console
will change resolution immediately. (It will also lose the nice-looking
GoboLinux font: to reload it, type `setfont lode-2.0-lat1u-16`.)

Now, you can start Xorg normally with:

```fish
startx
```

If you want to resize your VirtualBox window, make sure "Auto-resize guest
display" is turned on in the VirtualBox "Machine" menu, then, after resizing the
VirtualBox window, type in the GoboLinux terminal the following

```xorg
xrandr --output VGA-0 --preferred
```

This will resize the desktop to match your window size.

Note that this installation of the VirtualBox guest additions will only last for
the current Live-CD session. If you install GoboLinux into a VirtualBox virtual
hard drive, you will have to do the same again.
