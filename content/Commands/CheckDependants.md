---
title: "CheckDependants"
---

```
NAME
       CheckDependants -

SYNOPSIS
       CheckDependants <program> [<version>]

DESCRIPTION
       Find which applications is dependant on a given application.

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

       -f, --fast

              Do a fast check - do not cross check result with ldd.

       -s, --specific-version

              Be more specific regarding given version. May miss some applications.

       -m, --include-minors

              Use the version given as base, and include any minor and bug release versions when checking.

   Notes:
              If no version is given, current version, or latest version, if no current version is found, is used.

EXAMPLES
              CheckDependants Cairo 1.0.2

COPYRIGHT
       Copyright © 2007 Jonas Karlsson - Released under the GNU GPL.

GoboLinux                                                March 2017                                       CHECKDEPENDANTS(1)

```
