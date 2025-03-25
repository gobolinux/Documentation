---
title: "VerifyProgram"
---

```
NAME
       VerifyProgram -

SYNOPSIS
       VerifyProgram { [<options>] <<package> [<version>] | <tarball>> }

DESCRIPTION
       Verify the hashes file gpg signature and check the hashes of a Gobolinux package.

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

       -r, --keyring <entry>

              GPG option to an additional the keyring location.

       -S, --no-signature

       Just verify FileHash.
              Do not check GPG signature.

       -q, --quiet

       No output.
              Check exit status for result.

       -W, --no-web

              Do not check remote keyserver for keys.

   Notes:
              If no version is specified, Current is assumed.

   The default keyrings are:
              /Users/root/.gnupg/pubring.gpg /Programs/Scripts/Current/Data/gpg/goboring.gpg

COPYRIGHT
       Copyright © 2003 Carlo Calica. Released under the GNU GPL.

GoboLinux                                                March 2017                                         VERIFYPROGRAM(1)
```
