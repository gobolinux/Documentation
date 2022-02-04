---
title: "UnionSandbox"
---

```
NAME
       UnionSandbox -

SYNOPSIS
       UnionSandbox [<options>] <program> [<command-parameters...>]

DESCRIPTION
       Run the program in a protected sandbox, as superuser, using unionfs

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

       -w, --writedir <entry>

              The dir where writes outside sandbox are written.

       -d, --directory <entry>

              The program should be run at <entry>. This path should be either absolute, or relative to the sandbox root.

       -s, --sandbox <entry>[:<entry>...]

              Colon-separated list of areas where the restricted process has write access to.  The default value is '.'.

       -m, --map <entry>[:<entry>...]

              Colon-separated mapping (lhs=rhs) where writes to rhs are mapped to lhs.

       Notes:

       To allow mobility within the sandbox, the '.' directory is mounted at a sandbox root (like ). For this reason, use of
       relative paths like '..' to reach directories higher in the hierarchy than '.' may produce  unexpected  results.   It
       may also confuse symbolic links that flow through the sandbox.

EXAMPLES
              UnionSandbox -r 0.0 -s '.:/Programs/NaughtyApp/Current' make install

COPYRIGHT
       Copyright © 2003. Released under the GNU GPL.

GoboLinux                                                March 2017                                          UNIONSANDBOX(1)

```
