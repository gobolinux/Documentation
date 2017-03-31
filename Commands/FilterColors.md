```
NAME
       FilterColors -

SYNOPSIS
       FilterColors

DESCRIPTION
       Filter to monochrome.

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

   Notes:
              Piping  output  through  FilterColors  removes terminal escape codes (which usually define color, but may have
              other uses).

EXAMPLES
              FilterColors is usually used through a pipe: some_command | FilterColors

GoboLinux                                                March 2017                                          FILTERCOLORS(1)

```
