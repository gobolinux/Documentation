---
title: "Running under GNOME Boxes"
linkTitle: "GNOME Boxes"
weight: 1
---

GNOME Boxes is a new virtual machine manager and remote desktop manager powered
by QEMU, KVM, and libvirt virtualisation technologies. Running Gobolinux under
GNOME Boxes is quite easy, even more so than under Virtualbox.

## Setup Instructions

1. Create a new Virtual Machine by clicking "New" in the top left corner.
2. Click "Select a file".
3. Select the Gobolinux LiveCD ISO file.
4. Boxes will be ready to create a virtual machine with 2GB of RAM and 21.5GB of
   storage. If that is sufficient, click "Create".
5. Otherwise you can click "Customize" and adjust the sliders for RAM and
   storage respectively, then click the back arrow.
6. The LiveCD session will then start. Continue normal installation procedures.
   Remember to eject the LiveCD prior to reboot by going to the top right menu
   and clicking "Properties" -> "Devices & Shares" and then clicking "Remove"
   beside the CD/DVD section.

## Installing SPICE

Spice allows for integration with the host system including setting native
resolutions, file transfers, clipboard support etc.

1. Compile `SPICE-VDAgent`
2. Run `StartTask Spice-VDAgent` after login
3. Run `spice-vdagent`
4. Run `xrandr --output Virtual-0 --preferred` to update the resolution
