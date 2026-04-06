---
title: "Compile.conf"
weight: 1
---

`Compile.conf` is the file where you can configure the various paths and URLs used
by [`Compile`]({{%relref "Compile" %}}).

It is stored at `/Programs/Compile/Settings/Compile/Compile.conf` -- which, once
installed, has a link at `/System/Settings/Compile/Compile.conf` (if you're used
to the GoboLinux tree, you should know by now that this is the same as
`/etc/Compile/Compile.conf`).

These are the usual contents of the file:

Your name here so that credit is added to recipes.

```shell
compileRecipeAuthor="Paul McCartney"
# example only! change the name (unless of course, you're Paul ;) )
```

The standard locations for your local `Compile` files.

```shell
compileArchivesDir="$compileDir/Archives"
compileSourcesDir="$compileDir/Sources"
compileRecipeDirs="$compileDir/Recipes"
```

Some of the main free software repositories are treated especially: recipes use
these variables in their `url` declarations, so that you can pick your favorite
mirror without having to edit recipes one by one:

```shell
ftpGnu=ftp://ftp.gnu.org/gnu/
ftpAlphaGnu=ftp://alpha.gnu.org/gnu/
httpSourceforge=http://unc.dl.sourceforge.net/sourceforge/
```

The `Compile` recipe tree is managed by Git. The git repository and the upstream
branch are both configurable through the following variables:

```shell
compileRecipesRepository=https://github.com/gobolinux/Recipes.git
compileUpstreamBranch=master
```

A variable to set the `make` command called by `Compile`. `ColorMake` provides the
highlighting that GoboLinux has by default:

```shell
compileMakeCommand="ColorMake"
```

Next, you many define options to use with the `make` command. This is especially useful
if you want to run `make` multi-threaded on multicore CPUs (or for other customisation).

For instance on an 8-thread CPU you might set:

```shell
compileMakeOptions="-j8"
```

Note that this will fully occupy your CPU, so if you want use your system while
compiling, it might be better to reserve a few cpu threads (eg `-j6`).