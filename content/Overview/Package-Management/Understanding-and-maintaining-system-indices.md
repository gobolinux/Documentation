---
title: "Understanding and Maintaining system indices"
menuTitle: "Understanding system indices"
weight: 2
---

The two main parts of GoboLinux are `/Programs` and `/System`. If you stick to
using [`InstallPackage`](/Commands/InstallPackage) and
[`Compile`](/Commands/Compile), these two parts will be implicitly kept in sync
by [`SymlinkProgram`](/Commands/SymlinkProgram). But a lot of power lies in the
fact that you can tune how these two worlds interact.

Program entries under `/Programs` feature a `Current` symlink pointing to a
specific version that is "active" in the system. This `Current` version is taken
as the default version when you don't specify a version in scripts, and the link
is updated when you install a new version with
[`InstallPackage`](/Commands/InstallPackage) or [`Compile`](/Commands/Compile).

That doesn't mean that you can only have one version linked into the system: you
can have files of multiple versions show up in `/Programs`. In fact, when you
install a new version with [`InstallPackage`](/Commands/InstallPackage) but keep
the old version in `/Programs`, files for which there's no version with the same
name in the new package are still linked -- this is especially useful for
libraries.

For example, say program `Foo 1.0` looks like this:

    /Programs/Foo/1.0/bin/foo
    /Programs/Foo/1.0/include/foo.h
    /Programs/Foo/1.0/lib/libfoo.so.1
    /Programs/Foo/1.0/lib/libfoo.so -> libfoo.so.1

Now, say, you install a new version, 2.0, which looks like this:

    /Programs/Foo/2.0/bin/foo
    /Programs/Foo/2.0/include/foo.h
    /Programs/Foo/2.0/lib/libfoo.so.2
    /Programs/Foo/2.0/lib/libfoo.so -> libfoo.so.2

The default behavior of [`SymlinkProgram`](/Commands/SymlinkProgram) is to
replace symlinks under `/Programs` that belong to a different version of the
same program. So, now, we'll have the following links related to Foo under
system:

    /System/Index/bin/foo -> /Programs/Foo/2.0/bin/foo
    /System/Index/include/foo.h -> /Programs/Foo/2.0/include/foo.h
    /System/Index/lib/libfoo.so.2 -> /Programs/Foo/2.0/lib/libfoo.so.2
    /System/Index/lib/libfoo.so -> /Programs/Foo/2.0/lib/libfoo.so.2
    /System/Index/lib/libfoo.so.1 -> /Programs/Foo/1.0/lib/libfoo.so.1

So, now, when you run `foo`, it will fetch version `2.0` of the program through
your system `$PATH` (which looks at `/System/Index/bin`). But, as you can see,
`libfoo.so.1` is still there. This way, if you have other programs installed in
the system that are linked specifically to version 1 of the libfoo library will
continue working.

This means you won't have the old problem "I upgraded package Foo and now my
other apps are broken". Of course, you can still break things when you _remove_
a version which other programs depend in (or if buggy programs link to a version
independent name of a library (`libfoo.so`) but depend on features of a specific
version).

Besides [`SymlinkProgram`](/Commands/SymlinkProgram) (see section
"[Compiling manually](/Howtos/Manual-Compile/)" and its
[ reference entry](/Commands/SymlinkProgram) for details on it), there are other
scripts that give you more control over what is linked in the system and what is
not.

With [`DisableProgram`](/Commands/DisableProgram), you can remove from `/System`
all links that refer to a specific version of a program, effectively "turning it
off" -- it is as if it were not present in the system.

With [`RemoveProgram`](/Commands/RemoveProgram), you can remove a program from
`/Programs` and its references from `/System` in a single step.

See [Removing programs](/Overview/Package-Management/Removing-programs/) for
more details.
