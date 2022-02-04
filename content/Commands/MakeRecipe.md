---
title: "MakeRecipe"
---

```
NAME
       MakeRecipe -

SYNOPSIS
       MakeRecipe  {{[<app_name> [<app_version>]] <url>} | {<app_name> cvs <server> <module>} | {<app_name> svn <svn url>} |
       {<app_name>

DESCRIPTION
       Create a recipe template.

       git <repository>} | {<app_name> bzr <branch>} | {<app_name> hg <repository> }

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

       -F, --no-fetch

              Do not try to download the package. Assume it is already present.

       -C, --no-check

              Do not check for existing recipes for that program.

       -b, --batch

              Do not ask for confirmation.

   Notes:
              A URL, a cvs, svn, git, bzr or hg command line should be passed as a parameter.

EXAMPLES
              MakeRecipe Help2Man  1.33.1  http://ftp.gnu.org/gnu/help2man/help2man_1.33.1.tar.gz  MakeRecipe  DirectFB  cvs
              :pserver:anonymous:@cvs.directfb.org:/cvs/directfb    DirectFB   MakeRecipe   SYSLINUX   git   http://www.ker‐
              nel.org/pub/scm/boot/syslinux/syslinux.git

COPYRIGHT
       Copyright © 2003, Hisham Muhammad - Released under the GNU GPL.

GoboLinux                                                March 2017                                            MAKERECIPE(1)

```
