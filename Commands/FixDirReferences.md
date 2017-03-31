```
NAME
       FixDirReferences -

SYNOPSIS
       FixDirReferences <files...>

DESCRIPTION
       Converts .{la,pc,cmake} files created by libtool/pkgconfig/cmake to make them GoboLinux-compliant.

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

       -b, --backup

              Keep a backup file of the original files before modifying them.

EXAMPLES
              FixDirReferences -b *.la *.pc *.cmake

COPYRIGHT
       Copyright © Hisham H. Muhammad et al, 2003-2007. Released under the GNU GPL.

GoboLinux                                                March 2017                                      FIXDIRREFERENCES(1)

```
