---
title: "Binary packages"
weight: 2
---

> [!WARNING] We do not maintain a binary package repository at this time!
> Please build your packages from source using [`Compile`]({{%relref Compiling-from-source %}})!

**Binary packages** in GoboLinux are precompiled software packages built for the
GoboLinux directory tree and made available through the GoboLinux software
repository (recipe store). Since these packages are already compiled, you can
save the many hours needed to build larger applications. On the other hand, with
binary packages you don't have the ability to set compile flags for optimization
or specific architectures.

## Installing packages

[`InstallPackage`]({{%relref "InstallPackage" %}}) is the GoboLinux script for
installing binary packages. If you want
[`InstallPackage`]({{%relref "InstallPackage" %}}) to look for the most recent Gimp
package available, you can run

```fish
InstallPackage Gimp
```

The script will check if the package is available in the GoboLinux repositories.
(See `/System/Settings/GetAvailable.conf` for the specific URLs scanned. You may
add your own repositories if you desire.)

If you want to select a specific version, you can pass it as the second
parameter:

```fish
InstallPackage Gimp 3.2.2
```

If you downloaded the package and want to install it, run:

```fish
InstallPackage Gimp--3.2.2--x86_64.tar.bz2
```

The script normally runs interactively, asking about each dependency of the
requested package before installing it. You can avoid these queries by adding
the `--batch` or `-b` flag. This is particularly useful with large packages such
as Gimp or Xorg, which have many dependencies.

```fish
InstallPackage -b Gimp
```

### Dependencies

`InstallPackage` will warn you if dependencies of a package you are trying to
install are unavailable and ask if you want to continue. This is valuable,
because some software may still work satisfactorily even if a particular plug-in
or other dependency is missing.

## Installing packages from the LiveCD

See [Installing Packages from the
LiveCD]({{%relref "Installing-packages-from-the-LiveCD" %}}).

## Removing packages

See [Removing programs]({{%relref "Commands" %}}Removing-programs/).
