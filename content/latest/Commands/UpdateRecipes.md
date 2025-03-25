---
title: "UpdateRecipes"
---

```
NAME
       UpdateRecipes -

SYNOPSIS
       UpdateRecipes [<program>]

DESCRIPTION
       Update local recipe list from recipe stores.

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

       -a, --all

              Download  contents  of updated recipes. By default, UpdateRecipes will only fetch the recipe list and generate
              empty recipe directories (except when updating a single program).

       -l, --all-latest

              Like --all, but only fetch the latest versions of each recipe.

       -t, --thorough

              Check all availabe mirrors for updates. By default, only the first  working  mirror  (as  configured  in  Com‐
              pile.conf) is used.

   Notes:
              When  updating  a  single  program,  UpdateRecipes will download all its available recipes. When no program is
              specified, UpdateRecipes will fetch the recipe list and populate  with directory  entries  (and  download  the
              recipes only if --all is used).

       (C) 2003-2004 Carlo Calica et al. Released under the GNU GPL.

GoboLinux                                                March 2017                                         UPDATERECIPES(1)
```
