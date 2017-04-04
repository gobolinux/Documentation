In short: What makes GoboLinux unique?
--------------------------------------

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

      
    /System/Index/Executables/ping  
    /System/Index/Libraries/libpng.so.3  

Traditional Unix paths are also symlinks to the `/System/Index`
directory structure:

      
    /bin -> /System/Index/Executables  
    /usr/bin -> /System/Index/Executables  
    /usr/lib -> /System/Index/Libraries  

So for example, a shell script expecting to run `/usr/bin/ping`, will
continue to find it under GoboLinux.

This architecture -- installing each program under its own directory,
and making executables, headers other resources available via symlinks
-- has significant advantages:

-   different versions of libraries can coexist
-   it's trivial to uninstall software
-   there is no need for a package database.

In fact, the scope of the task of managing software with this
organization is so constrained that most utility programs needed to
adminster the system could be reasonably implemented as shell scripts,
which GoboLinux developers chose to do.

Managing dependency relations among software is accomplished through the
[GoboLinux build system](Compiling-from-source) and its library of ["compile
recipes"](Recipe).

