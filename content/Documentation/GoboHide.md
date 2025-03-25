---
title: "GoboHide"
---

To simplify the users' view of filesystem, GoboHide conceals legacy unix
directories such as `/usr`, `/lib`, `/sbin`, and `/etc`, which contain links to
files placed elsewhere under [The GoboLinux Filesystem
Hierarchy]({{%relref "GoboLinux-Filesystem-Hierarchy" %}}).

GoboHide works by hooking directory read operations directly in the root of the
problem: since every `readdir()` call is translated and performed by the kernel,
we have added a list which is kept in kernel, checking every `readdir()`
operation. If the current inode being read is stored in this list, then it
simply doesn't get copied onto the destination buffer, which should be returned
to the user.

The user's interface to the GoboHide ioctl's is through a userspace tool, called
**`gobohide`**, and has the following options:

```
gobohide --help

gobohide: Hide/Unhide a directory

-h, --hide     Hide the directory
-u, --unhide   Unhide the directory
-l, --list     List the hidden directories
--version  Show the program version
--help     Show this message
```

In order to hide a directory, one would need to run gobohide with `-h`, passing
the target entry. A subsequent `ls` will not show the hidden entry, then:

```
ls /

Depot  Mount     System bin  etc  proc  sys  usr
Files  Programs  Users  dev  lib  sbin  tmp  var

gobohide -h /usr
gobohide -h /etc

ls /

Depot  Mount     System  bin  lib   sbin  tmp
Files  Programs  Users   dev  proc  sys   var
```

This allows entries to be _really_ hidden from the filesystem. But don't worry,
this can be only performed by the superuser, and he/she has power to ask the
kernel for the entries being hidden. This ensures that nothing gets hidden
without the superuser's conscience:

```
gobohide -l

Hidden directories:
/etc
/usr
```

And the best of it all: you can still access your files inside these hidden
entries, and even bash would tell you that files exist in these directories:

```fish
if [ -f /etc/fstab ]; then echo "okay"; fi
okay

ls /etc/zshrc

rwxrwxrwx  28 /etc/zshrc -> /Programs/ZSH/Settings/zshrc
========================================================
28 in 1 file - 7614808 kB used (96%), 388760 kB free
```

GoboHide currently supports hiding entries on any mounted filesystem. Because it
is implemented at the level of the Linux virtual filesystem, it is independent
of specific filesystems.
