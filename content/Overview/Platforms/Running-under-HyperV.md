---
title: "Running under HyperV"
menuTitle: "HyperV"
weight: 4
---

When running the GoboLinux 016.01 live ISO through Hyper-V, you will
notice that `startx` does not start correctly by default. You can fix
this by adding a kernel boot parameter and creating an Xorg
configuration file.

Edit `/System/Kernel/Boot/grub/grub.cfg` and find the kernel boot line.
Change `video=vesafb:off` to `video=hyperv_fb:1024x768` and save it. You
may wish to try this part in advance first, without saving it; in that
case, press "e" at the Grub menu, make this same edit, and press Ctrl-X
to boot once only with the new command line.

Run `X -configure`. It will generate a file `xorg.conf.new`. Edit this
file, and change `vesa` to `fbdev`. Move the file to `/etc/X11/xorg.conf`.

Reboot. `startx` will now work normally.

