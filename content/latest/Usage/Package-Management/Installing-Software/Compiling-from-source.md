---
title: "Compiling from source"
weight: 1
---

### Introduction

With **Compile**, GoboLinux build utility, software sources can be downloaded,
compiled and installed in a single step. An example will follow next.

In order to install **irssi**, a text-based IRC client from the command line,
you would type the following instruction:

```fish
Compile irssi
```

Depending on the speed of your computer, internet connection and what packages
you have installed, Irssi should download and install in a few minutes.

**Compile** manages the build process using GoboLinux recipes. Each recipe contains
a list of build directives and supplemental control files for compiling a
particular software library.

Recommended blog articles to read on **Compile**:
 - [The ideas behind Compile](https://gobolinux.org/doc/articles/compile.html)
 - [Compile: the GoboLinux compilation system](https://gobolinux.org/compile.html)

### Finding recipes

Typically, you can just try the name of the recipe you want from the command
line. There is also an [online recipe viewer](http://recipes.gobolinux.org),
listing the most recently uploaded recipes first.

### Command-line options

Compile has a number of command-line options, which are [listed
here]({{%relref "Compile" %}}). The following are especially useful.

When using the `--batch` or `-b` automatically attempts to process all
dependencies of the requested program.

### Separating download and compile phases

The next two options are useful when working with intermittent internet access,
or if you'd like to run your compiling jobs at night when you're asleep.

Calling Compile with the `--no-build` flag downloads sources only.

Later, in the event that you wish to use the `--no-web` flag, this will direct
Compile to search to your system's own download cache and build the sources
found there instead. This commandline switch is obviously very useful if you do
not have a working internet connection for the time being.

### Writing recipes

_Main article:_ [Writing recipes]({{%relref "Writing-Recipes" %}})

### Getting the latest Compile

To use the version of Compile, run

```fish
cd /Programs/Compile/Current
git pull && UpdateSettings --auto Compile
```
