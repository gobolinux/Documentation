---
title: "FetchArchive"
---

```
NAME
       FetchArchive -

SYNOPSIS
       FetchArchive <recipe> [arch-recipe]

DESCRIPTION
       Given a recipe, download the files required to compile it.

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

       -d, --save-directory <entry>

              Rename the directory into which the archive is unpacked/files checked out.

       -s, --save-to <entry>

              Save the files to the given directory

       -P, --program <entry>

              Program name The default value is 'Bash'.

       -V, --version-number <entry>

              Version number with revision The default value is '4.0-r1'.

       -b, --batch

              Avoid asking questions.

EXAMPLES
              FetchArchive /K3B/0.10/Recipe

GoboLinux                                                March 2017                                          FETCHARCHIVE(1)
```
