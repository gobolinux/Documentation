---
title: "Resources/"
weight: 8
---

The Recipe subdirectory `Resources/` can contain various metadata. These files
are copied to `/Programs/Foo/Version/Resources` upon installation. All these
files are optional except for `Dependencies` and `Description`.

### `BuildDependencies`

This file lists dependencies which must be present to successfully compile the
Program. They may include compilers or build tools. The format is the same as
Dependencies, below.

*Example:*

```fish
Autoconf 2.60
Automake 1.11
GTK-Doc 1.9 [doc]
Intltool 0.35.0
LibTool 2.4.0
Pkgconfig 0.20
Vala [vala]
```

### `BuildInformation`

Informational file about which versions of dependencies were actually linked
against when compiling.

### `Defaults/`

This is a directory which may contain, in `Defaults/Settings`, the default
contents of the `/Programs/Foo/Settings` directory. The contents of this
directory will be reconciled with the currently active settings, if any, by
[`UpdateSettings`]({{%relref "UpdateSettings" %}}). The original defaults will
remain in `/Programs/Foo/Version/Resources/Defaults`, so that a user may revert
to them as necessary.

`Defaults/` may also contain a subdirectory `Variable/`. These files are copied
to `/System/Variable/`, if not already present.

### `Dependencies`

This file lists programs which should be installed for this Program to work
properly. The format is like

```fish
Fontconfig 2.4.2
FreeType 2.1.10
GCC >= 3.0.0, < 4.0.0, != 3.1.0
Glibc 2.5
Lame >= 3.96.1 [lame]
Mesa 6.5.2
Qt >= 3.3.8, < 4.0 [qt]
LuaRocks:luafilesystem
CPAN:XML::Parser
Xorg 7.2
ZLib 1.2.3
```

The tags such as `[lame]` specify [Use Flags]({{%relref "Use-flags" %}}), optional
dependencies which affect the compilation of the package, if present.

When the range string (i.e., `=`, `>=`, etc) is omitted, the dependency
resolution algorithm assumes it to be `>=`.

The exact algorithm for complex dependencies is specified in
[`CheckDependencies`]({{%relref "CheckDependencies" %}}) but allows for a sequence
of options separated by `|` (or) each of which is a sequence of versions
separated by "," (and). Precedence is left to right. Thus:

```fish
GCC < 4.0.0 | >= 4.1.0, != 4.1.2 | ICC > 2.0.0
```

means a GCC version less than 4.0.0 or a GCC version greater than 4.1.0 but not
equal to 4.1.2 or an ICC version greater than 2.0.0. See the code for
[`CheckDependencies`]({{%relref "CheckDependencies" %}}) for the exact algorithm.

Dependencies to language-specific package managers can be fulfilled using the
[Aliens](https://github.com/gobolinux/AlienVFS) subsystem, using the syntax
`AlienType:alien_package`, as in the examples above.

Note that there are limitations in version handling for Aliens, as it depends on
the Alien provider and the package manager itself:

-   CPAN dependencies ignore version information
    ([CPAN only installs the latest version](http://stackoverflow.com/questions/260593/how-can-i-install-a-specific-version-of-a-set-of-perl-modules))

For more info, see [Dependencies](#dependencies) and [Use
Flags]({{%relref "Use-flags" %}}).

### `Description`

This file contains information of interest to humans regarding the program. A
typical example is

```
[Name] GCC
[Summary] The GNU Compiler Collection
[Description] The GNU Compiler Collection contains frontends for C,  C++,
Objective-C, Fortran, Java, and Ada...
[License] GNU General Public License (GPL)
[Homepage] http://gcc.gnu.org/
```

### `Environment`

This file contains environment variables which should be set for this program,
as bash assignments. For example, the Firefox recipe has

```shell
export MOZ_PLUGIN_PATH=${goboLibraries}/browser-plugins
```

### `Hints`

These contain hints for `UpdateSettings` on when to overwrite, delete, or skip
updating of certain settings. See [[Hints File]].

### `PostInstall`

A bash script which is executed by [`Compile`]({{%relref "Compile" %}}) (or
[`InstallPackage`]({{%relref "InstallPackage" %}})) after installation. This is for
one-time actions which should not be associated with any stage of the
compilation or installation process, but run after the Program is symlinked.
They are kept separate from the Recipe file so that they are retained in binary
packages which may be distributed.

### `Requirements`

These list conditions that must be met on the system, but which do not entail an
action unless they're not met. The only implemented requirements so far are
`required_users` and `required_groups`.

Entries in `required_groups` can have a gid parameter, as seen in this example:

```fish
required_groups=(
  "users"
  "yes gid=90125"
)
```

Individual entries in `required_users`, on the other hand, can have `uid=<num>`
and `groups=<name[,name]*>` options, as in:

```fish
required_users=(
  "scripts"
  "wakeman uid=2112 groups=yes,users"
)
```

### `Tasks/`

Files in this subdirectory are [boot script
tasks]({{%relref "Boot-script-tasks" %}}), linked to `System/Tasks`. These are
roughly equivalent to the `/etc/init.d` scripts found in many distributions.

Note that files under `System/Tasks/` should be marked as executable! Otherwise
they will fail to execute during boot time!

### `Wrappers/`

This subdirectory contains scripts which are typically GoboLinux-specific
wrappers for commands in the installed package. They may call the real program
with options or environment appropriate for a GoboLinux system. They are linked
into the `/System/Index/bin` directory along with the normal binaries.
