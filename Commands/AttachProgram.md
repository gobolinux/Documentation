```
NAME
       AttachProgram -

SYNOPSIS
       AttachProgram <program> [<version>] [<src_tree>]

DESCRIPTION
       Create a link in /Programs to $goboInstall or <src_tree>.

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

              Batch mode.

       -f, --force

              Force, reattach even if installed.

       -r, --rootfs

              Move to RootFS.

       -D, --no-dependencies

              Do not try to fullfit dependencies.

   Notes:
              This  script creates a program entry in /Programs with a version symlink to <src_tree> directory.  After it is
              tied into /Programs, SymlinkProgram is executed.  If <destdir> is omitted the env var goboInstall is used.

EXAMPLES
              AttachProgram GCC 2.95.3 /Network/Programs

COPYRIGHT
       Copyright © 2004 Carlo Calica. Released under the GNU GPL.

GoboLinux                                                March 2017                                         ATTACHPROGRAM(1)

```
