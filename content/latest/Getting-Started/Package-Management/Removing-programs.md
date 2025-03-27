---
title: "Removing programs"
weight: 3
---

In GoboLinux, all programs, whether binary packages or user-compiled software,
are installed into a single directory under the `/Programs` hierarchy, such as,
for instance, gimp:

```fish
/Programs/Gimp/2.8.18
```

Removing this program can be, in theory, as simple as:

```fish
rm -rf Gimp/2.8.18 
```

But since this leaves behind dangling symlinks, GoboLinux offers the
[`RemoveProgram`]({{%relref "RemoveProgram" %}}) utility, which removes the program
and all links pointing to its files in `/System/Index`.

```fish
RemoveProgram Gimp 2.8.18
```

Sometimes you may want to "turn off" a program temporarily, without erasing it
from your hard disk. In other words, you want to remove program's executables
from the execution path, and remove libraries and headers from the lookup path.

In GoboLinux, this can be accomplished by removing the associated symlinks for
`/System/Index`. The DisableProgram script facilitates this:

```fish
DisableProgram gimp 2.1.18
```

The version parameter given here, in this case `2.1.18`, is optional. If it is
not provided, the `Current` link is used to determine the program version to
disable. Also note that the program name is case insensitive, but it appears to
be simpler to use a downcased variant - easier to type at the least.

To re-enable the program, all you need to do is recreate the symbolic links:

```fish
SymlinkProgram gimp 2.1.18
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
