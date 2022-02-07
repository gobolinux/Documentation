---
title: "NamingConventions"
---

```
NAME
       NamingConventions -

SYNOPSIS
       NamingConventions <name>

DESCRIPTION
       Heuristics to determine a capitalized, GoboLinux-like name.

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

GoboLinux                                                March 2017                                     NAMINGCONVENTIONS(1)
```

Note that NamingConventions is part of the `Scripts` package. You can find in
the `bin/` subdirectory there.

Here are some usage examples; note that presently NamingConventions appears to
prefer only the program name, so if you have a full remote URL, make sure to
only pass the name of the program towards NamingConventions.

```fish
NamingConventions glib => GLib
```
