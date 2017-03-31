```
NAME
       MergeTree -

SYNOPSIS
       MergeTree <source> <destination>

DESCRIPTION
       Mirrors one directory structure into another.

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

       -d, --delete

              On conflicts, overwrite original file.

   Notes:
              All files and directories in <source> appear as symbolic links in <destination>

EXAMPLES
              MergeTree /Programs/KOffice/Current /Programs/KDE/Current

GoboLinux                                                March 2017                                             MERGETREE(1)

```
