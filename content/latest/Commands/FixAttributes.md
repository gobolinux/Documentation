---
title: "FixAttributes"
---

```
NAME
       FixAttributes -

SYNOPSIS
       FixAttributes [options...] files...

DESCRIPTION
       Fix attributes from files based on its contents.

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

       -R, --recursive

              Recurses into subdirectories fixing permissions.

       -t, --true <entry>

              Sets permission <entry> if file is considered executable.

       -f, --false <entry>

              Sets permission <entry> if file is considered not executable.

   Notes:
              Default permission modes are obtained from FixAttributes.conf.

COPYRIGHT
       Copyright © Hisham Muhammad, 2000-2003 - Released under the GNU GPL.

GoboLinux                                                March 2017                                         FIXATTRIBUTES(1)
```
