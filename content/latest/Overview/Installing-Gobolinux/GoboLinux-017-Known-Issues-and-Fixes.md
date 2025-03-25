---
title: "GoboLinux 017 Known Issues and Fixes"
linkTitle: "Known Issues and Fixes"
weight: 1
---

### Outstanding issues

Some problems have been reported by our users and are currently being fixed by
our team. They are:

-   Copy-and-paste does not work out of the box from a VM. Compiling
    `spice-vdagent` and loading its daemon should fix that.
-   Sometimes when trying to `Compile` an already-installed Program, the build
    process will fail (see
    [Compile bug 51](https://github.com/gobolinux/Compile/issues/51)). Sometimes
    this can be worked around by first manually doing a
    `RemoveProgram <failing program>` before re-attempting to `Compile` it. Note
    that it is generally a _**Bad Idea™**_ to try to `RemoveProgram`, say,
    `Python3` like this as it will break `Compile`.
-   `ContributePackage` is not working -- use
    [ContributeRecipe]({{%relref "GitHub-contributor-workflow" %}}) instead.
