---
title: "NewVersion"
---

```
NAME
       NewVersion -

SYNOPSIS
       NewVersion <package> <version> (url)

DESCRIPTION
       Update a recipe to a new version.

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

       -s, --source <entry>

              Recipe version number to use as a base for the new version

       -n, --former-name <entry>

              App name of the Recipe to use as a base. Only necessary if it's different from the name of the new Recipe

       -k, --keep-existing

              Keep existing recipe if one already exists

   Notes:
              Optimistically,  it  assumes only the version number has changed, and the compilation process is still identi‐
              cal. The generated recipe is better understood as a 'template' for the new version recipe.

EXAMPLES
              NewVersion Allegro 4.1.12, NewVersion --source 0.9.7 Wine 0.9.14

COPYRIGHT
       Copyright © 2003, Hisham Muhammad - Released under the GNU GPL.

GoboLinux                                                March 2017                                            NEWVERSION(1)

```

Usage example:

  NewVersion Bash 4.4.12

