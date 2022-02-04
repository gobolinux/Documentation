---
title: "SandboxInstall"
---

```
NAME
       SandboxInstall -

SYNOPSIS
       SandboxInstall [<options>] <program_name> <program_version> [ -- <extra_arguments> ]

DESCRIPTION
       Runs 'make install', using a sandbox environment.

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

       -t, --target <entry>

              Makefile target to be used.  The default value is 'install'.

       -f, --makefile <entry>

              Specify which makefile to use.  The default value is 'Makefile'.

       -m, --make <entry>

              Use  the given variant of make (ie: cmake). Use in recipe_type={makefile,configure} The default value is 'Col‐
              orMake'.

       -c, --command <entry>

              Use the given command instead of make (ie: python). Options --target and --makefile are then ignored.

       -a, --add-allowed <entry>

              Specify additional allowed directories or files. Colon separated list.

       -u, --unmanaged-files <entry>

              Specify allowed directories or files, which should be handled as unmanaged. Colon separated list.

       -F, --no-sandbox

              Do not protect the installation with a sandbox.

       -e, --expand-sandbox <entry>

              By default, the sandbox is built relative to the current directory, '.'. Passing 1 to this option  will  build
              it relative to the parent directory, '..',passing 2 relative to '../..', and so on.

       -l, --allow-leftovers

              When using UnionFS, do not return a failure code when it catches files outside the sandbox.

       Notes:

       Normally you'll want to use Compile(1) instead.  'SandboxInstall' is called by Compile(1).

EXAMPLES
              SandboxInstall --makefile makefile.unix --target install_shared WeirdSuperLib 2.4

COPYRIGHT
       Copyright © Hisham Muhammad, 2001-2005 - Released under the GNU GPL.

GoboLinux                                                March 2017                                        SANDBOXINSTALL(1)

```
