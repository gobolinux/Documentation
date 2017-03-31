```
NAME
       UnversionExecutables -

SYNOPSIS
       UnversionExecutables [<options>] <program_name> [<program_version>]

DESCRIPTION
       Delete versioned hardlinks for each executable created by VersionExecutables

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

       -a, --all-versions

              Remove links for all versions of a program, not just Current (when no version specified).

   Notes:
              This tool will only remove links created by VersionExecutables and listed in Resources/VersionExecutables.

EXAMPLES
              UnversionExecutables ZSH 4.3.6

COPYRIGHT
       Copyright © 2008 Michael Homer. Released under the GNU GPL version 2 or later.

GoboLinux                                                March 2017                                  UNVERSIONEXECUTABLES(1)

```
