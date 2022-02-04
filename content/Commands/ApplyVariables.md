---
title: "ApplyVariables"
---

```
NAME
       ApplyVariables -

SYNOPSIS
       ApplyVariables

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

       -o, --open <entry>

              Opening mark.  The default value is '@%'.

       -c, --close <entry>

              Closing mark.  The default value is '%@'.

       -i, --identifier <entry>

              Add a prefix identifier in the form of '<entry>_' to the opening markup.

   Notes:
              ApplyVariables processes a file replacing instances of variables marked

       with special indicators ('@%', '%@' by default) with the contents of equivalent environment variables.

GoboLinux                                                March 2017                                        APPLYVARIABLES(1)

```
