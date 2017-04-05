GoboLinux has a directory structure different from other Linux
distributions. In GoboLinux, all files for a program, including
executables, headers and libraries, are installed below a single
directory that belongs to that program. So the `ping`
utility might reside in

      
    /Programs/Netkit-Base/0.17/bin/ping  

and `libpng.so.3` in

    /Programs/LibPNG/1.2.5/lib/libpng.so.3  

To be visible to other software, these files are symlinked into standard
locations in the new directory hierarchy under `/System/Index`:

      
    /System/Index/bin/ping  
    /System/Index/lib/libpng.so.3  

Traditional Unix paths are also symlinks to the `/System/Index`
directory structure:
      
    /bin     -> /System/Index/bin  
    /usr/bin -> /System/Index/bin  
    /usr/lib -> /System/Index/lib  
    /etc     -> /System/Settings

As a result, most things just work. For example, GoboLinux will
correctly dispatch scripts with shebang lines such as
`#!/usr/bin/env perl` or `#!/usr/bin/python` to the proper
interpreter.

This architecture -- installing each program under its own directory,
and making executables, headers other resources available via symlinks
-- has significant advantages:

-   different versions of libraries can coexist
-   it's trivial to uninstall software
-   there's no need for a database of installed files

The system is administered through a limited set of
[utility programs](GoboLinux-Command-Reference).
Tracking dependency relations among software is accomplished
through the [GoboLinux build system](Compiling-from-source)
and its library of ["compile recipes"](Recipe).
