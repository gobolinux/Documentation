---
title: "Replacements for standard commands"
---

GoboLinux has its own replacements for a few standard commands like `su` and
`make`. The reasons for making a replacement ranges from adding necessary
functionality (`su`) to making prettier output (`make`).

While having these "replaced programs" is not a problem in itself (in fact, most
provide enhanced functionality which adds to the GoboLinux experience), it's
important to point out these differences here so that you can know what's going
on with these perhaps unexpected behaviors.

The replacements are provided by several different packages. All except
`install` are handled by making an alias in the shell initialization scripts.
This way, you can easily disable the alias and restore the original version of a
program, if you so wish. They can be often found in their own subdirectory
Resources/Wrappers inside the program directory.

-   su - aliased to Su in the Shadow package to handle names other than root as
    super user
-   sudo - aliased to Sudo in the Sudo package to handle names other than root
    as super user
-   top - aliased to htop in the Htop package
-   make - aliased to [`ColorMake`]({{%relref "ColorMake" %}}) in the Scripts
    package to produce colorful output
-   info - aliased to Info in the Pinfo package
-   man - aliased to Man in the Pinfo package
-   install - install in CoreUtils has been renamed to real_install with install
    in the Scripts package as a wrapper (see section [Sandboxing under
    GoboLinux]({{%relref "Sandboxing-under-GoboLinux" %}}) for a detailed
    explanation)
-   which - the Scripts package provides a "which" script which resolves
    symlinks in the path of the returned program, so that it indicates the
    /Programs path the binary refers to.

Aliases enabling "enhanced replacements" such as Htop and Pinfo are set in the
Environment section of these packages. This way, if you want to stick to plain
`top` and/or `info`, all you need to do is to remove (or just not install) these
replacements.
