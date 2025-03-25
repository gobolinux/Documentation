---
title: "DisableProgram"
---

```
NAME
       DisableProgram -

SYNOPSIS
       DisableProgram <program> [<version>]

DESCRIPTION
       Unlink a program from the /usr hierarchy.

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

       -u, --unmanaged <entry>

              Defines  what to do with unmanaged files from package.  Valid entries are: 'ask' 'remove' 'keep' 'interactive'
              The default value is 'ask'.

   Notes:
              This script 'disables' a program in the system, while keeping it in the /Programs  hierarchy.  To  're-enable'
              it, run SymlinkProgram(1) again. If version is not specified, Current is assumed.

EXAMPLES
              DisableProgram GCC 2.95.3

COPYRIGHT
       Copyright © 2003 Hisham Muhammad. Released under the GNU GPL.

GoboLinux                                                March 2017                                        DISABLEPROGRAM(1)
```
