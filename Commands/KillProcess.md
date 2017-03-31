```
NAME
       KillProcess -

SYNOPSIS
       KillProcess { -c | -m | [-n] <regexps...> }

DESCRIPTION
       Enhanced process killing utility.

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

       -i, --interactive

              Ask for confirmation before killing a process.

       -d, --display

              Informative output only. Do not actually kill any process.

       -n, --name

              Kill  processes  by  name.  This is similar to killall, but names are matched to regular expressions passed as
              additional parameters to KillProcess. This is the default behavior if no other mode switches are passed.

       -m, --memory

              Kill the process that is consuming the greatest amount of memory.

       -c, --cpu

              Kill the process with the highest CPU usage level.

       -s, --spare <entry>[:<entry>...]

              Enter a colon-separated list of program names that should not be killed by automatic kills. Entries  for  this
              list can also be added in the killProcessSpare entry in the configuration file.

   Notes:
              Be  mindful  that  when  matching processes by name, you are actually searching for a match in any part of the
              entire process command line. For example, entering 'ion' as a pattern would also match  'evolution'.  Further‐
              more, even parameters may match: a search for 'lpd' would also kill 'kwrite helpdocument.txt'.

EXAMPLES
              KillProcess knotify artsd kwrited

COPYRIGHT
       Copyright © 2003. Released under the GNU GPL.

GoboLinux                                                March 2017                                           KILLPROCESS(1)

```
