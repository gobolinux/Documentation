---
title: "Filesystem Virtualization with Runner"
menuTitle: "Virtualization with Runner"
weight: 1
---

[Runner](/Commands/Runner) is a utility for launching programs under GoboLinux
that ensures that the filesystem view of a process will match its dependencies. 
In other words, Runner eliminates the possibility of library conflicts when
running an executable.

Runner is a filesystem virtualization tool that sets up a
constrained view of `/System/Index` for a process based on the
executable program's `Dependencies` file.  It is run as a
wrapper, e.g. `Runner SomeApp`.

Runner builds a custom mount table for the process, like
container tools do, but without duplicating files. It
dynamically picks the correct parts of your `/Programs` tree.
This approach is feasible in GoboLinux due to way programs
are each confined to their own subdirectories. 

# Preparing the filesystem view

All you have to do is to make sure the dependencies of the program you want to run are correctly listed under the program's [[Resources directory|Recipe-Format-Specification#resources]] - more specifically, in the [[Dependencies|Recipe-Format-Specification#dependencies]] file at `/Programs/Name/Version/Resources/Dependencies`. You may list program names (e.g., `LibPNG`), specify a particular version (as in `LibPNG 1.4.4`) or even let Runner pick the best version given a certain range (e.g., `LibPNG >= 1.4.0, < 1.5.0`).

Most likely, the program you want to run will already have a sane `Dependencies` file - every binary package we distribute will have one, just like every compilation recipe do.

# The Compile tool

Compile makes use of Runner to control the environment
for building software packages. When you type `Compile Foo`,
Compile fetches the recipe for Foo and passes both the
`Dependencies` and `BuildDependencies` files of that recipe to
Runner. This ensure that the right versions of
the libraries, headers, and executables needed by that
package will be mapped onto `/System/Index`.

# Spawning an application with Runner

For regular GoboLinux packages, simply type `Runner application_name`. Runner will figure from which entry under `/Programs` `application_name` comes from, and will create a custom filesystem view for that application by overlaying its dependencies over `/System/Index`.

For non-regular GoboLinux packages, such as third-party executables downloaded on your home directory, you can hand-craft a `Dependencies` file and then provide that file to Runner, as in `Runner -d MyDependenciesFile ./third_party_app`.

# Multi-arch setups

Running a 32-bit application on a 64-bit distro is no different with Runner. Provided that you have the 32-bit dependencies installed under `/Programs` (such as `Glibc/2.18-i686` and `Bash/3.1-i686`), the Dependencies file of your program simply needs to state the versions of the 32-bit packages it relies on. Afterwards, simply type `Runner application_name` and you are all set.
