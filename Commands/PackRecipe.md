```
NAME
       PackRecipe -

SYNOPSIS
       PackRecipe [<program> [<version>]]

DESCRIPTION
       Generate "packed recipes", ready for submission.

OPTIONS
       --terse

              Enable terse messages.

       --debug

              Enable debug messages.

       -h, --help

              Show this help.

       --version

              Show program version.

       -v, --verbose

              Enable verbose mode.

       --logfile <entry>

              Log all output to specified file.

       -L, --no-lint

              Do not verify recipes (not recommended).

       -W, --no-web

              Offline operation when running RecipeLint (avoid if possible).

   Notes:
       Given no arguments, this script will take all recipes in
              and pack them as Foo--1.0--recipe.tar.bz2 files at .

       (C) 2003-2004 Carlo Calica et al. Released under the GNU GPL.

GoboLinux                                                March 2017                                            PACKRECIPE(1)

```
