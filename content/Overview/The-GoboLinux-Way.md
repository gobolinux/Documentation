---
title: "The GoboLinux Way"
weight: 2
---

## Welcome to GoboLinux

The main task of a Linux distribution is to keep track of and organize
the programs in your computer, so that they work properly. GoboLinux is
no different from the others in this goal, but it adopts a fundamentally
different approach in solving this problem. Instead of scattering the
files of programs around, following the [decades-old
conventions](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)
of ancient UNIX systems, and then adding a layer of control (a "package
manager") to try to give order to chaos, in GoboLinux we organize the
files that comprise the programs in an ordered way in the first place.

In GoboLinux, every program lives in its own subdirectory. Under the top
level directory `/Programs`; e.g you'll find Xorg 7.0 at
`/Programs/Xorg/7.0`, and ping at `/Programs/Netkit-Base/0.17/bin/ping`.
To see what programs are installed in the system, all you need to do is
look in the `/Programs` directory:

```fish
ls /Programs
```

For each category of files, there is a directory under `/System/Index`
grouping files from each application as symbolic links: `bin`, `lib`,
`libexec`, `include`, `share`, and `man`. For compatibility, each
"legacy" UNIX directory is a link to a corresponding category.
Therefore, `/bin`, `/sbin`, `/usr/bin`, `/usr/local/bin` (and so on) are
all symlinks to entries under `/System/Index`.

In short, what we have is a database-less package management system: the
directory structure itself organizes the system. Wasn't that its
original purpose, after all? Each program directory (for example,
`/Programs/KDE`) holds version directories (`/Programs/KDE/3.4`,
`/Programs/KDE/3.4.2`), and a version-neutral directory for settings
(`/Programs/KDE/Settings`), to keep files that would normally be in
`/etc`. Keeping two or more versions of a library is trivial: upgrading
LibPNG to 1.2.8 means adding `/Programs/LibPNG/1.2.8`, but does not
automatically imply that LibPNG 1.2.7 is removed. This way, if a program
depends on the previous version, it won't break. As you can see,
GoboLinux gives you a finer control of what is and isn't in the system.

Historical tidbit: *When most distributions switched to GCC 3 they
released a new major version, mostly incompatible with previous ones. In
contrast, when the 006 series of GoboLinux adopted GCC 3, compatibility
was preserved by simply keeping old versions of libraries alongside the
new ones, while they were gradually phased out. No "compat" packages
were needed.*

## The "legacy" tree

Unfortunately, not all programs have the flexibility to be installed
anywhere. Occasionally, hardcoded paths creep in even in programs that
belong to userland, and should, at least theoretically, allow themselves
to be installed inside, say, a user's home directory.

As much as we'd like to see this done in the long term, patching all
applications is not an option. For this reason, GoboLinux keeps, as
stated earlier, a legacy tree where all usual Unix paths are mapped to
GoboLinux equivalents. That way, if a Makefile looks for
`/usr/X11R6/include/X11/Xaw3d/XawInit.h`, it will find it, although it
is really at `/Programs/Xaw3d/1.5/include/X11/Xaw3d/XawInit.h`, where it
belongs. When two applications have a directory entry with the same
name, the GoboLinux scripts recursively expand them. Both Xorg and Xaw3d
have X11 under `include`. A directory `/System/Index/include/X11` is
created automatically, holding links from both X11 directories.

Another interesting feature is that the GoboLinux scripts execute
`make install` using a special user id that only has write permissions
inside the program's source directories and the program's entry under
`/Programs`. This way, files can't "escape" from the GoboLinux hierarchy
and slip a directory into the legacy tree.

A detail that might surprise you at first is that when you look at the
root directory (with `ls` or graphical tools), you don't see the legacy
directories, even though you can `cd` into them. They are certainly
there — they are just kept hidden using [GoboHide](/Documentation/GoboHide),
a kernel modification designed to conceal the legacy tree from the usual
system view. (GoboHide is of course optional — GoboLinux works just as
well using standard Linux kernels.)

## Influences and roots

As you read this, you have probably found many familiar concepts (not to
mention directory names). GoboLinux has clearly found inspiration in
other operating systems, like NeXT, BeOS and AtheOS, but it was the
notion that they build "something different" using an existing Unix base
(be it using a BSD foundation as in macOS, or using GNU tools as in
AtheOS) was the most important influence of all. There are several other
projects, in various stages of development, that use the Linux kernel as
a foundation and feature alternative directory trees. Interestingly,
most of them are clones or heavily inspired by a specific proprietary
operating system. (At different points in time, we've seen clones of
RiscOS, NeXT, BeOS.)

GoboLinux, on the other hand, is not a clone of anything else. It uses
standard Linux desktop software. We believe that the well-organized
directory structure makes it a good testbed for new ideas —
possibilities are wide open (see the forum and moreso the mailing list
for discussions, and to a lesser extent the IRC channel `#gobolinux` on
libera.chat).

## Differences between GoboLinux and a traditional Linux system

What follows is not a thorough description of GoboLinux, but a quick
cheat-sheet of facts that are good to know when you are getting
acquainted to the system.

-   In the GoboLinux hierarchy, files are grouped by their functional
    category (executables, libraries, and so on). There are links at the
    classic directories you are used to (`/bin`, `/usr/bin`, and so on), but
    remember that they all point to the same place. This is a huge
    advantage, as it means, for example, that you'll never have to
    search for a library throughout your filesystem again -- it will
    always be in `/lib` (and in `/usr/lib`, because they point to the same
    place! -- no worries about compatibility).

-   There are symbolic links relating most of the usual UNIX directories
    to the GoboLinux tree. Therefore, you will find directories such as
    `/etc`, `/var/log` and `/usr/bin` in the expected places. However, some
    directories, such as the users' directories, didn't need to be
    linked to their "legacy" locations. This way, for a given user
    called "joe", you'll have, instead of `/home/joe`, `/Users/joe`. Notice
    also that the superuser's directory is no different than the ones
    from the other users, so, root's directory is at `/Users/root`. Mount
    points are under `/Mount`, not `/mnt`.

-   Another major difference between GoboLinux and most Linux
    distributions is that it does not use a BSD nor a System V
    initialization procedure. Instead, it has its own. At
    `/System/Settings/BootScripts` you will find
    a few files that command the entire boot procedure: BootUp and
    Shutdown run at system boot and shutdown, respectively; you can
    define custom "runlevel" scripts to define different ways you want
    your system to be initialized (say, Single and Multi for single and
    multi-user, Graphical for boot into graphic mode, etc.) and control
    that from the boot loader menu. The `/System/Settings/BootOptions`
    file separate site-specific settings from the rest of the scripts.
    You can also find a library of application specific tasks at
    `/System/Tasks` that can be used during boot (those are installed by
    the apps).

For a better overview of how it looks and feels right, nothing beats
giving the Live CD a spin. You'll be running a full GoboLinux system
without having to install anything. Just burn a CD-ROM and give it a go!
