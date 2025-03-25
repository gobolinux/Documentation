---
title: "Dependencies blacklist"
weight: 4
---

## Configuring Dependencies

Today there are many programs implementing a given feature in different ways.
One such example is the OpenGL API, with implementations floating in packages
such as Xorg, MesaLib and Nvidia. However, not every user owns a Nvidia card,
and here comes a problem: how should one mask Nvidia from the automated
Dependencies list generated after creating a recipe? This problem is now fixed
with a configurable file called
`/Programs/Scripts/Settings/Scripts/Dependencies.blacklist`.

### Dependencies.blacklist

This file allows one to specify packages that should not appear in the
Dependencies file after creating a new recipe. Its format is pretty simple: one
package per line, without the need to specify its version.

#### A `Dependencies.blacklist` example

The following example blacklists the packages `Glibc` and `Nvidia`. Comments and
blank lines are ignored by the parser, so it's ok to include them.

```fish
# Dependencies.blacklist is documented in detail at
#  http://wiki.gobolinux.org/Dependencies

Glibc
Nvidia
```

Note: presently blacklisting specific versions is not supported, but the same
behaviour can be achieved by creating an empty directory in the `/Programs`
directory. For example, to blacklist `GCC` version `4.1.2` you may:

```fish
mkdir /Programs/GCC/4.1.2
```
