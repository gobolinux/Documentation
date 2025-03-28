---
title: "Getting Started"
weight: 1
chapter: false
pre: "<b>001&thinsp;</b>"
---

## Welcome to the world of GoboLinux !

The main task of a Linux distribution is to keep track of and organize the
programs in your computer, so that they work properly. **GoboLinux** is no different
from the others in this goal, but it adopts a fundamentally different approach
in solving this problem.

Instead of scattering the files of programs around,
following the
[decades-old conventions](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)
of ancient UNIX systems, and then adding a layer of control (a "package
manager") to try to give order to chaos, in **GoboLinux** we organize the files that
comprise the programs in an ordered way in the first place.

In **GoboLinux**, every program lives in its own subdirectory. Under the top level
directory `/Programs`; e.g you'll find Xorg 7.0 at `/Programs/Xorg/7.0`, and
ping at `/Programs/Netkit-Base/0.17/bin/ping`. To see what programs are
installed in the system, all you need to do is look in the `/Programs`
directory:

```fish
ls /Programs
```

For each category of files, there is a directory under `/System/Index` grouping
files from each application as symbolic links: `bin`, `lib`, `libexec`,
`include`, `share`, and `man`. For compatibility, each "legacy" UNIX directory
is a link to a corresponding category. Therefore, `/bin`, `/sbin`, `/usr/bin`,
`/usr/local/bin` (and so on) are all symlinks to entries under `/System/Index`.

In short, what we have is a database-less package management system: the
directory structure itself organizes the system. Wasn't that its original
purpose, after all? Each program directory (for example, `/Programs/KDE`) holds
version directories (`/Programs/KDE/3.4`, `/Programs/KDE/3.4.2`), and a
version-neutral directory for settings (`/Programs/KDE/Settings`), to keep files
that would normally be in `/etc`.

Keeping two or more versions of a library is
trivial: upgrading LibPNG to 1.2.8 means adding `/Programs/LibPNG/1.2.8`, but
does not automatically imply that LibPNG 1.2.7 is removed. This way, if a
program depends on the previous version, it won't break. As you can see,
**GoboLinux** gives you a finer control of what is and isn't in the system.

Historical tidbit: _When most distributions switched to GCC 3 they released a
new major version, mostly incompatible with previous ones. In contrast, when the
006 series of GoboLinux adopted GCC 3, compatibility was preserved by simply
keeping old versions of libraries alongside the new ones, while they were
gradually phased out. No "compat" packages were needed._

## Getting Started Topics:

{{% children depth="2" %}}