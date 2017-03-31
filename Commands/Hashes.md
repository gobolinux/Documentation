```
NAME
       Hashes -

SYNOPSIS
       Hashes { [-c] <package> [<version>] }

DESCRIPTION
       Manages FileHash and FileHash.sig in a GoboLinux package.

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

       -c, --check

              check the package's dependency file

       -s, --sign

              Generate, then sign the hash file

       -g, --generate

              Generate the hash file.

       -l, --list

              List hash file, if any (generate if not present).

       -u, --local-user <entry>

              Use <entry> as the user ID to sign with.

       -r, --keyring <entry>

              GPG option to an additional the keyring location.

   Notes:
              If no version is specified, Current is assumed.

COPYRIGHT
       Copyright © 2003 Carlo Calica. Released under the GNU GPL.

GoboLinux                                                March 2017                                                HASHES(1)

```
