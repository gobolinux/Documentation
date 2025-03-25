---
title: "DetachProgram"
---

```
NAME
       DetachProgram -

SYNOPSIS
       DetachProgram <program> [<version>] [<destdir>]

DESCRIPTION
       Move a program from /Programs to $goboInstall or <destdir>.

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

       -c, --copy

       Copy program.
              Keep existing on rootfs.

       -b, --batch

       Batch operation.
              Minimize warning output

       -D, --no-dependencies

              Do not try to fulfill dependencies.

   Notes:
              This  script  'moves' a program from the /Programs hierarchy to <destdir> directory.  Afterwards, symlinks are
              created in /Programs to maintain functionality.  If <destdir> is omitted the env var goboInstall is used.

EXAMPLES
              DetachProgram GCC 2.95.3 /Network/Programs

COPYRIGHT
       Copyright © 2004 Carlo Calica. Released under the GNU GPL.

GoboLinux                                                March 2017                                         DETACHPROGRAM(1)
```
