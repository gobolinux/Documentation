---
title: "ListProgramFiles"
---

Gives you the list of files which belong to some program you have installed on your machine.

Which files belong the current installed version of
`Wireless-Tools`?
```fish
ListProgramFiles wireless-tools
```

or, equivalently: 
```fish
ListProgramFiles wireless-tools Current
```

Which files belong to version 28 of `Wireless-Tools`?
```fish
ListProgramFiles wireless-tools 28
```

Notice how `<program>` field is not case-sensitive although `<version>` field is. 
 
Which files belong to all versions of `Wireless-Tools`?
```fish
ListProgramFiles /Programs/Wireless-Tools
```

Notice that we passed the program's directory instead of its name. 

```
NAME
       ListProgramFiles -

SYNOPSIS
       ListProgramFiles <program> [<version>] | <version_directory>

DESCRIPTION
       List files from a program in a 'clean' way, skipping some file patterns.

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

       -f, --files

              List files (equivalent to -xtype f in 'find')

       -l, --links

              List links (equivalent to -type l in 'find')

       -R, --no-resources

              Do not list files in Resources directory

       -p, --path

              Return full path, including the programs directory

       -n, --null

              Separate files with null instead of newline.

COPYRIGHT
       Copyright © 2006. Released under the GNU GPL.

GoboLinux                                                March 2017                                      LISTPROGRAMFILES(1)
```
