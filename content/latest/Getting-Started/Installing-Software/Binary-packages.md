---
title: "Binary packages"
weight: 3
---

{{% notice warning %}} We do not maintain a binary package repository at this time! |
Please build your packages from source using [`Compile`]({{%relref Compiling-from-source %}})! {{% /notice %}}

**Binary packages** in GoboLinux are precompiled software packages built for the
GoboLinux directory tree and made available through the GoboLinux software
repository (recipe store). Since these packages are already compiled, you can
save the many hours needed to build larger applications. On the other hand, with
binary packages you don't have the ability to set compile flags for optimization
or specific architectures.

## Installing packages

[InstallPackage]({{%relref "InstallPackage" %}}) is the GoboLinux script for
installing binary packages. If you want
[InstallPackage]({{%relref "InstallPackage" %}}) to look for the most recent Gimp
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
InstallPackage Gimp 2.8.18
```

If you downloaded the package and want to install it, run:

```fish
InstallPackage Gimp--2.8.18--i686.tar.bz2
```

The script normally runs interactively, asking about each dependency of the
requested package before installing it. You can avoid these queries by adding
the `--batch` or `-b` flag. This is particularly useful with large packages such
as Gimp or Xorg, which have many dependencies.

```fish
InstallPackage -b Gimp
```

### Dependencies

InstallPackage will warn you if dependencies of a package you are trying to
install are unavailable and ask if you want to continue. This is valuable,
because some software may still work satisfactorily even if a particular plug-in
or other dependency is missing.

## Installing packages from the LiveCD

See [Installing Packages from the
LiveCD]({{%relref "Installing-packages-from-the-LiveCD" %}}).

## Removing packages

See [Removing programs]({{%relref "Commands" %}}Removing-programs/)

## Creating packages

### Structure

In GoboLinux, all binary packages (as well as all user-compiled software) is
installed under `/Programs` in a "program directory" provided for each version
of each application, for example:

```fish
/Programs/Gimp/2.8.18
```

When compiling software under GoboLinux the installation target directories such
as `bin/`, `lib/`, and `etc/` that are required for a typical program are placed
inside the program directory.

With this self-contained directory structure, all that is needed to generate a
binary package is to make a tarball of the program directory, copy over the
`Resources/` directory from the Compile recipe, and generate a few additional
files, which are also placed under `Resources/`.

This is accomplished by the [CreatePackage]({{%relref "CreatePackage" %}}) command.

### Preparation

Before creating a package, be careful to vet the contents of the program's
`Settings/` directory to ensure that it does not include personal information.

A package submitted for inclusion in the GoboLinux packages repository must have
sensible default settings, honoring the application defaults if possible.

### The CreatePackage command

In order to create a package, run the
[CreatePackage]({{%relref "CreatePackage" %}}) utility with the package name as a
parameter. For example,

```fish
CreatePackage rxvt
```

will create a binary package in the current working directory.
