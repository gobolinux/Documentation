---
title: "Sandboxing under GoboLinux"
---

The **build system** in GoboLinux uses sandboxing to ensure that all the
filesystem writes during the software install phase are limited to an
appropriate part of the filesystem. GoboLinux 016 ships with two different
sandbox implementations.

[UnionSandbox]({{%relref "UnionSandbox" %}}) is a modern implementation which uses
file system unions to achieve isolation. It is the default sandbox installer.

**FiboSandbox** is a fallback method used when a union-filesystem implementation
is not available in the running kernel. It sets up an isolated environment and
commands are run by a special user (named `fibo`) without root privileges.

During the installation phase of the software build process, most build systems
call the `install` program to copy files to their destination directories with
the proper ownership and attributes. `install` belongs to the `CoreUtils`
package.

Since user **fibo** lacks authority to change file ownership, the link at
`/System/Index/bin/install` points to a wrapper script in the `Scripts` package.

Under **UnionSandbox**, this wrapper script translates the superuser name if
necessary and calls `real_install`, a symlink to the CoreUtils `install`
utility, passing along the modified arguments.

Under **FiboSandbox**, the wrapper discards change-of-owner directives before
calling `real_install`.

[GoboLinux dark corners]({{%relref "GoboLinux-dark-corners" %}})
