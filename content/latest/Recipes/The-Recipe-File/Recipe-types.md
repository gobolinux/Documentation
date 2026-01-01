---
title: "Recipe Types"
weight: 2
---

Supported recipe types (also known as modes), to be given as argument to
`recipe_type`:

## configure

###### **`recipe_type=configure`**
is used for Programs based on "configure" scripts,
(autoconf or not.) Some options are only relevant for *configure*:

###### **`configure_options=(<array of options>)`**

Flags to be passed to the configure script. These flags are passed in addition
to default flags detected by [`PrepareProgram`]({{%relref "PrepareProgram" %}})
(such as `--prefix` and `--sysconfdir` on autoconf-based configure scripts), unless
the `override_default_options` declaration is used.

###### **`autogen_before_configure=yes`**

Use it if you need to run `./autogen.sh` in order to generate the configure
script.

### autogen

The program to run for the above. Defaults to `autogen.sh`.

###### **`configure=<program name>`**

By default the configure script is assumed to be called `configure`. Use this
variable to override this value. Remember that the current directory during
execution will still be the one set by the `dir` variable, even if a directory
path is given (as in the second example below). If the behavior you intended is
for Compile to `cd` to the `unix` directory and run its build sequence there,
use `dir` instead.

Examples (only one applies at a time):

```fish
configure=Configure.gnu
configure=unix/configure
```

## cabal

###### **`recipe_type=cabal`**
is used for Programs based on *Cabal*, the package manager for Haskell. Some
options are only relevant for *cabal*:

###### **`cabal_options=(<array of options>)`**

Flags to be passed to the Cabal configure operation.

These flags are passed in addition to default flags detected by
[`PrepareProgram`]({{%relref "PrepareProgram" %}}) (such as `--prefix`) unless the
`override_default_options` declaration is used.

### runhaskell

Specifies the method of invoking Haskell to perform a Cabal-based compilation.
The default is `runhaskell`.

## cmake

###### **`recipe_type=cmake`**
is used for Programs based on CMake. Some options are
only relevant for `cmake`:

###### **`cmake_options=(<array of options>))`**

Flags to be passed to the CMake configure operation. These flags are passed in
addition to default flags (such as `-DCMAKE_INSTALL_PREFIX`).

###### **`cmake_variables=(<array of assignments>)`**

Variables to be defined in the environment during the execution of cmake.

## makefile

###### **`recipe_type=makefile`**
is used for Programs based on Makefiles. No options
are relevant only for *makefile*.

## meson

###### **`recipe_type=meson`**
is used for Programs based on Meson. Some options are
only relevant for *meson*:

###### **`meson_options=(<array of assignments>)`**

Flags to be passed to the Meson setup operation.

## python

###### **`recipe_type=python`**
is used for Programs based on Python Distutils. Some
options are only relevant for *python*:

###### **`python_options=(<array of options>)`**

Array of options to be passed to the Python Distutils build script. This works
similarly to the `configure_options` array.

###### **`build_script=<name>`**

Specify the same for the Python build script. If none is given, Compile tries a
few default ones, such as setup.py.

## scons

###### **`recipe_type=scons`** 
is used for Programs based on SCons. Some options are
only relevant for *scons*:

###### **`scons_variables=(<array of assignments>)`**

Variables to be passed to scons.

## xmkmf

###### **`recipe_type=xmkmf`** 
is used for Programs based on X11 Imake. No options are
relevant only for *xmkmf*.

## manifest

###### **`recipe_type=manifest`** 
is used to directly copy appropriate files from the
archive into place. Some options are only relevant for *manifest*:

###### **`manifest=(<array "file:dir">)`**

Specify which files should be copied over, and to where. Destination is relative
to `target`.

Example:

```fish
manifest=(
   "some_script:bin"
   "include/a_header.h:include"
   "lib/libfoo.so:lib"
   "some_script.1:man/man1/some_script.1"
)
```

## meta

###### **`recipe_type=meta`** 
only depends on other Recipes. All included recipes are
built relative to the same installation prefix. Some options are only relevant
for *meta*:

###### **`include=(<array of recipes>)`**

In a meta-recipe, this array holds the list of recipes that should be built to
constitute the complete program. Recipe names should be in the format
`App--1.0`. The order of the entries in the array is significant, because it is
the order in which the recipes are built. 

> [!NOTE]
> Be careful with the order, because re-building a meta-package that's already
> installed may cover up ordering problems.

###### **`part_of=<parent>`**

Indicates that this recipe is generally included as part of a meta-recipe.
Unless Compile is called with `-i`/`--install-separately`, the Program will be
installed into the parent Program's directory. Implies `keep_existing_target`.

###### **`update_each_settings=yes`**

In meta-recipes, Compile only calls `UpdateSettings` for the meta-recipe and not
for its sub-recipes. Set this variable to override this behavior and have
`UpdateSettings` called in every sub-recipe.
