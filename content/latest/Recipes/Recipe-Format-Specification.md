---
title: "Recipe Format Specification"
weight: 1
---

This is the official specification document for the GoboLinux recipe format.

The term "Recipe" can refer to either:

-   A packed recipe, as held in GoboLinux recipe store, with a name like
    `Foo--1.0-r1--recipe.tar.bz2`.
-   The file `Foo/1.0-r1/Recipe` in such a tarball. This is also called the
    "recipe file".

## File Layout

A packed recipe is a tarball such as `SomeProgram--Version-r1--recipe.tar.bz2`
with the following directory structure.

```fish
SomeProgram/
   `--Version-r1/
        |-- Recipe               (required)
        |-- *.patch
        |-- *.patch.in
        |-- Resources/
        |     |-- Dependencies   (required)
        |     |-- Description    (required)
        |     |-- Defaults/
        |     |     |-- Settings/
        |     |     `-- Variable/
        |     |
        |     |-- Tasks/
        |     |-- Wrappers/
        |     |-- BuildDependencies
        |     |-- BuildInformation
        |     |-- Environment
        |     |-- Hints
        |     |-- PostInstall
        |     `-- Requirements
        |
        `-- <arch>/
              |-- Recipe
              `-- Resources/
```

where `<arch>` represents one or more optional architecture directories named
`i686/`, `x86_64/`, `arm/`, `ppc/`, etc.
