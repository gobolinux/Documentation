---
title: "BootDriver"
---

The `BootDriver` script should not be run directly from the command line. It is
intended to be specified in the `inittab` file (`/System/Settings/inittab`), to
be launched by process 1, `init`.

`BootDriver` takes a parameter, indicating which "runlevel" script should be
executed. Here's a sample `inittab` with calls to `BootDriver`:

```fish
id:2:initdefault:

l1:S:wait:/System/Index/bin/BootDriver BootUp
su:S:respawn:/sbin/sulogin

l2:12345:wait:/System/Index/bin/BootDriver Console
l6:6:wait:/System/Index/bin/BootDriver Reboot
l0:0:wait:/System/Index/bin/BootDriver Halt

ca:12345:ctrlaltdel:/sbin/shutdown -t1 -r now

1:2345:respawn:/System/Index/bin/agetty tty1 9600
2:2345:respawn:/System/Index/bin/agetty tty2 9600
3:2345:respawn:/System/Index/bin/agetty tty3 9600
4:2345:respawn:/System/Index/bin/agetty tty4 9600
5:2345:respawn:/System/Index/bin/agetty tty5 9600
```
