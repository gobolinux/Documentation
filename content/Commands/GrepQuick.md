---
title: "GrepQuick"
---

```
NAME
       GrepQuick -

SYNOPSIS
       GrepQuick <pattern> [<files...>]

DESCRIPTION
       Shorthand for 'grep'.

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

       -r, --recursive

              Recursive.

       -w, --whole-word

              Match whole words only.

       -C, --no-color

              Avoid coloring (for grep's that don't support it).

       -b, --binaries

              Also search binary files.

       Notes:

       Search  is  case  sensitive  only  if there is at least one uppercase character in the pattern.  Binary files are not
       searched unless --binaries is given.  Error messages are not displayed.  Line numbers are displayed.  If no files are
       specified, all files are selected (except in "source" mode, where *.[CcHh]* is selected instead).

COPYRIGHT
       Copyright © 2001-2002 Hisham Muhammad. Released under the GNU GPL.

GoboLinux                                                March 2017                                             GREPQUICK(1)

```
