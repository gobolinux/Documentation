---
title: "SystemFind"
---

```
NAME
       SystemFind -

SYNOPSIS
       SystemFind [<flags>] <search_pattern>

DESCRIPTION
       Special 'find' utility for searches in the /System hierarchy

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

       -e, --executables

              Search for executables in /usr/bin.

       -l, --libraries

              Search for libraries in /usr/lib.

       -i, --headers

              Search for include headers in /usr/include.

       -s, --settings

              Search for settings in /System/Settings.

       -m, --manuals

              Search for settings in /usr/share/man.

       -q, --quick

              Scan symlinks in /System only (may not find all files).

   Notes:
              If no flags are set, all four system locations are scanned.

EXAMPLES
              SystemFind -i -l freetype

COPYRIGHT
       Copyright © 2003-2005 Hisham Muhammad. Released under the GNU GPL.

GoboLinux                                                March 2017                                            SYSTEMFIND(1)

```
