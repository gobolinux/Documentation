---
title: "FindQuick"
---

```
NAME
       FindQuick -

SYNOPSIS
       FindQuick <file_to_search> [<path>]

DESCRIPTION
       find files.

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

              if <file_to_search> contains "*", it is used directly as an expression for the search. If not, "*" is added to
              the beginning and the end.  if <path> is not specified, the working directory is assumed.

EXAMPLES
              FindQuick "*.c" ..  FindQuick # Note the added quotes to avoid shell expansion.

GoboLinux                                                March 2017                                             FINDQUICK(1)

```
