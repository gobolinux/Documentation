---
title: "Runner"
weight: 8
---

[Runner]({{%relref "Runner" %}}) is a utility for launching programs under
GoboLinux that ensures that the filesystem view of a process will match its
dependencies. In other words, Runner eliminates the possibility of library
conflicts when running an executable.

Runner is a **filesystem virtualization tool** that sets up a constrained view of
`/System/Index` for a process based on the executable program's `Dependencies`
file. It is run as a wrapper, e.g. `Runner SomeApp`.

Runner builds a custom mount table for the process, like container tools do, but
without duplicating files. It dynamically picks the correct parts of your
`/Programs` tree. This approach is feasible in GoboLinux due to way programs are
each confined to their own subdirectories.

More info:
 - https://gobolinux.org/gobolinux016.html (Runner was released as part of GoboLinux 016)
 - https://www.gobolinux.org/doc/linuxdev-br2017/GoboLinux_Runner.pdf

Main article (How-To): [**Filesystem virtualization with Runner**]({{%relref "Filesystem-virtualization-with-Runner" %}})