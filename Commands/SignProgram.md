```
NAME
       SignProgram -

SYNOPSIS
       SignProgram { <package> [<version>] | <package_file> }

DESCRIPTION
       Generate and sign a hash file of a Gobolinux package with gpg.

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

       -u, --local-user <entry>

              Use <entry> as the user ID to sign with.

       -S, --no-signature

       Just create FileHash.
              No GPG signing.

   Notes:
       If no version is specified, Current is assumed.
              If the -u option isn't

              used, the first ID found in the secret keyring is used.

COPYRIGHT
       Copyright © 2003 Carlo Calica. Released under the GNU GPL.

GoboLinux                                                March 2017                                           SIGNPROGRAM(1)

```
