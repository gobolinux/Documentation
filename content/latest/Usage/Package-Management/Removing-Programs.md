---
LinkTitle: "Removing"
title: "Removing Programs"
weight: 3
---

In GoboLinux, all programs, whether binary packages or user-compiled software,
are installed into a single directory under the `/Programs` hierarchy, such as,
for instance, gimp:

```fish
/Programs/Gimp/3.2.2
```

Removing this program can be, in theory, as simple as:

```fish
rm -rf Gimp/3.2.2 
```

But since this leaves behind dangling symlinks, GoboLinux offers the
[`RemoveProgram`]({{%relref "RemoveProgram" %}}) utility, which removes the program
and all links pointing to its files in `/System/Index`.

```fish
RemoveProgram Gimp 3.2.2
```

Sometimes you may want to "turn off" a program temporarily, without erasing it
from your hard disk. In other words, you want to remove program's executables
from the execution path, and remove libraries and headers from the lookup path.

In GoboLinux, this can be accomplished by removing the associated symlinks for
`/System/Index`. The `DisableProgram` script facilitates this:

```fish
DisableProgram gimp 3.2.2
```

The version parameter given here, in this case `3.2.2`, is optional. If it is
not provided, the `Current` link is used to determine the program version to
disable. Also note that the program name is case insensitive, but it appears to
be simpler to use a downcased variant - easier to type at the least.

`DisableProgram` automatically appends a `-Disabled` tag to the version name,
so in our case folder `3.2.2` has been renamed to `3.2.2-Disabled`. This way,
you can easily distinuish disabled from enabled programs via the file system
alone.

To re-enable the program, all you need to do is recreate the symbolic links:

```fish
SymlinkProgram gimp 3.2.2-Disabled
```

## Maintaining symlinks

GoboLinux has a script called [`RemoveBroken`]({{%relref "RemoveBroken" %}}). that
removes dangling symlinks from `/System/Index` tree. It can be useful to run
after manipulating directories under `/Programs`.

[`RemoveBroken`]({{%relref "RemoveBroken" %}}) takes a list of files, and removes
those that are dangling symlinks. If no arguments are provided, the script takes
filenames from standard input (typically through a pipe).

The usual procedure to clean up dangling links, is

```fish
cd /System/Index
find | RemoveBroken
```

> [!INFO]
> GoboLinux actually performs this task automatically on any file system changes inside
> `/System/Index`. This is done via a [`Listener`](https://github.com/gobolinux/Listener)
> hook. Check out it's configuration file at `/System/Settings/listener.conf` for more insight.