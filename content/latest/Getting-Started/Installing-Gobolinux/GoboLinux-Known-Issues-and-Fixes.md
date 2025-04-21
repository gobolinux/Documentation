---
title: "GoboLinux 017.01 Known Issues and Fixes"
linkTitle: "Known Issues and Fixes"
weight: 9
---

## Fix grub install error

A last -minute bug has sneaked into our GRUB/GRUB-EFI recipe.

Please install the updated revision of GRUB/GRUB-EFI, before attempting to install GoboLinux from the LiveCD:
```fish
InstallPackage https://gobonextgen.org/Packages/017.01/GRUB--2.12-r1--x86_64.tar.bz2
InstallPackage https://gobonextgen.org/Packages/017.01/GRUB-EFI--2.12-r1--x86_64.tar.bz2
```
You will be prompted to update some settings. Select "U" on each prompt.

Now you can proceed the installation of GoboLinux 017.01 via our `Installer`.

## Other outstanding issues

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
