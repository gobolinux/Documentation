---
title: "AddUser"
---

```
NAME
       AddUser -

SYNOPSIS
       AddUser [<options>] <login>

DESCRIPTION
       Register a new user in this system.

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

       -c, --comment <entry>

              Text to be stored in the comment field of the UNIX password file.

       -f, --full-name <entry>

              User's full name.

       -r, --room-number <entry>

              User's office number.

       -w, --work-phone <entry>

              User's work phone.

       -h, --home-phone <entry>

              User's home phone.

       -o, --other <entry>

              User's home phone.

       -s, --shell <entry>

              User's default shell.  The default value is '/bin/zsh'.

       -p, --password <entry>

              Encoded user's password.

       -S, --skel

              Populate home directory with customized settings.

   Notes:
              User  information  such as full name and office number can be viewed with programs such as finger(1) and modi‐
              fied with chfn(1).

EXAMPLES
              AddUser -f 'Hisham Muhammad' lode

COPYRIGHT
       Copyright © 2003. Released under the GNU GPL.

GoboLinux                                                March 2017                                               ADDUSER(1)
```
