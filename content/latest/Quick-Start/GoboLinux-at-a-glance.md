---
title: "GoboLinux at a glance"
weight: 1
---

For a gentle infroduction we recommend you start by reading the following
historical articles, authored by GoboLinux founder Hisham Muhammad:

- [GoboLinux at a glance](https://gobolinux.org/at_a_glance.html)
- [The Unix tree rethought: an introduction to GoboLinux](https://gobolinux.org/k5.html)
- [I am not clueless](https://gobolinux.org/doc/articles/clueless.html)


## What makes GoboLinux unique

**GoboLinux** has a directory structure different from most other Linux
distributions. In **GoboLinux**, all files for a program, including executables,
headers and libraries, are installed below a single directory that belongs to
that program.

So the `ping` utility might reside in

    /Programs/InetUtils/1.9.4/bin/ping

and `libpng.so` in

    /Programs/LibPNG/1.6.37/lib/libpng.so

To be visible to other software, these files are symlinked into standard
locations in the new directory hierarchy under `/System/Index`:

    /System/Index/bin/ping
    /System/Index/lib/libpng.so

Traditional Unix paths are also symlinks to the `/System/Index` directory
structure:

    /bin     -> /System/Index/bin
    /usr/bin -> /System/Index/bin
    /usr/lib -> /System/Index/lib
    /etc     -> /System/Settings

As a result, most things just work. For example, GoboLinux will correctly
dispatch scripts with shebang lines such as `#!/usr/bin/env perl` or
`#!/usr/bin/python` to the proper interpreter.

This architecture —installing each program under its own directory, and making
executables, headers other resources available via symlinks— has significant
advantages:

-   different versions of libraries can coexist
-   it's trivial to uninstall software
-   there's no need for a database of installed files

The system is administered through a limited set of [utility
programs]({{%relref "Commands" %}}). Tracking dependency relations among software
is accomplished through the [GoboLinux build
system]({{%relref "Compiling-from-source" %}}) and its library of
["compile recipes"](/Recipes).

The next pages will guide you through the process of setting up a GoboLinux [Live Environment →]({{%relref "Live-Environment" %}})