---
title: "Creating Packages"
weight: 4
---

## Structure

In GoboLinux, all binary packages (as well as all user-compiled software) is
installed under `/Programs` in a "program directory" provided for each version
of each application, for example:

```fish
/Programs/Gimp/3.2.2
```

When compiling software under GoboLinux the installation target directories such
as `bin/`, `lib/`, and `etc/` that are required for a typical program are placed
inside the program directory.

With this self-contained directory structure, all that is needed to generate a
binary package is to make a tarball of the program directory, copy over the
`Resources/` directory from the Compile recipe, and generate a few additional
files, which are also placed under `Resources/`.

This is accomplished by the [`CreatePackage`]({{%relref "CreatePackage" %}}) command.

## Preparation

Before creating a package, be careful to vet the contents of the program's
`Settings/` directory to ensure that it does not include personal information.

A package submitted for inclusion in the GoboLinux packages repository must have
sensible default settings, honoring the application defaults if possible.

## The `CreatePackage` command

In order to create a package, run the
[`CreatePackage`]({{%relref "CreatePackage" %}}) utility with the package name as a
parameter. For example,

```fish
CreatePackage rxvt
```

will create a binary package in the current working directory.
