---
title: "PrepareProgram"
---

```
NAME
       PrepareProgram -

SYNOPSIS
       PrepareProgram <target_name> <version_nr> [ -- <additional_options> ]

DESCRIPTION
       prepares applications for instalation, running the 'configure' script.

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

       -b, --batch

              batch mode: no user interaction

       -t, --tree

              Prepare directories only, do not attempt to run configure.

       -T, --tree-cleanup

              Like --tree, but instead of creating directories, remove empty ones

       -k, --keep

              Keep the directory if it already exists in the directory hierarchy.

       -r, --remove

              Remove the directory if it already exists in the directory hierarchy.

       -c, --configure <entry>

              Specify program to be used as 'configure' script.  The default value is './configure'.

       -a, --autoconf

              Assume configure is based on autoconf, skipping detection.

       -A, --no-autoconf

              Assume configure is NOT based on autoconf, skipping detection.

       -D, --no-default-options

              Skip detection altogether, use only configure options passed on the command-line.

   Notes:
              The directory hierarchy for the program is only created with --tree.

EXAMPLES
              PrepareProgram KDE 2.2

COPYRIGHT
       Copyright © 2001-2005 Hisham Muhammad - Released under the GNU GPL.

GoboLinux                                                March 2017                                        PREPAREPROGRAM(1)

```
