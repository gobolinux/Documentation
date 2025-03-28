---
title: "Other directives"
weight: 3
---

#### compile_version=\<version-number>

_Valid modes: all_

The version number of Compile used to create this recipe.

#### environment=(\<array of variables>)

_Valid modes: all_

Environment variables to be applied to the shell where the compilation takes
place. Each entry of the array must be in the format `variable=value`.

Example:

```fish
environment=(
   "PYTHONOPTIMIZE=2"
)
```

#### uncompress=no

_Valid modes: all_

Used for urls where the files are going to be used directly. Not a common
option.

#### unpack_files

_Valid modes: all_

_Possible values:_ `inside_first, contents_inside_first, dirs, files_in_root`.

Relevant when `files=(more than one file to download)` is used, or when a single
archive has "loose files" without an enclosing directory.

By default, all entries in `files` are unpacked in the same directory. This flag
can be used to override this behavior. `inside_first` tells it to unpack
`files[0]` and then unpack all subsequent files inside the resulting directory.

`contents_inside_first` tells it to unpack `files[0]`, then unpack the remaining
files, and move the contents of the resulting unpacked `dirs` into the first
directory.

`dirs` tells it to use the directories explicitly specified in the `dirs` array
as destinations for each file.

For example, if `files` is (foo.tar.gz bar.tar.gz) and foo.tar.gz contains

```
foo/1      foo/2
```

and bar.tar.gz contains

```
foo/3      bar/4      bar/5
```

The default unpacking behavior, without redefining `dirs` explicitly, generates:

```
foo/1      foo/2      foo/3      bar/4      bar/5
```

`unpack_files=inside_first` generates

```
foo/1      foo/2      foo/foo/3      foo/bar/4      foo/bar/5
```

`unpack_files=contents_inside_first` generates

```
foo/1      foo/2      foo/3      foo/4      foo/5
```

Using `dirs`, virtually any path structure can be used. Since the first entry in
the `dirs` array is special, it is not used by `unpack_files`. If any of the
`dirs` entries contains the value of the `target` array, the
`keep_existing_target` is implied (it can still be explicitly overridden in the
recipe, but then the user might delete the data that was just unpacked).

Using `files_in_root`, Compile assumes files are stored in the archive without a
directory. A directory is created so that files are unpacked inside it, avoiding
scattering files in $compileSourcesDir (typically `/Data/Compile/Sources`).

#### dir=\<directory>

#### dirs=(\<array of directories>)

_Valid modes: all_

Indicates the directory to `cd` into after the package is unpacked. If not
specified, the name of the package file (stripped of its extension) is assumed.
If `dirs` is used instead of `dir`, `dirs` is expected to contain the same
number of entries as `urls`. The first entry in the array is special: the
compilation method is applied only on the first directory. To compile multiple
packages into a single program, use meta-packages (`is_meta`). The usage of
`dirs` affects the way files are unpacked. See `unpack_files` for details.

#### docs=(\<array of filenames>)

_Valid modes: all_

A list of filenames, relative to the program's sources root, of files to be
copied to the program's `doc/` dir (or `doc/$app/` for meta-packages). Wildcards
are supported but must be single-quoted. Note that some default names such as
README\*, AUTHORS and TODO are automatically fetched.

Example:

```fish
docs=(
   'docs/*.html'
)
```

#### create_dirs_first=yes

_Valid modes: configure, makefile_

By default, Compile only generates directories in the target location right
before the installation step. This is useful for the --no-install option (see
the [Compile]({{%relref "Compile" %}}) reference entry). Unfortunately, some
programs fail during the configuration of compilation step if the target
directory does not already exist. Use this entry to appease those programs.

#### keep_existing_target=yes

_Valid modes: all_

When set, it will not ask the user if they want to erase the contents of the
$target (if any) prior to compiling the program. This is implicitly set if the
`dirs` array contains any reference to `target`. See `unpack_files` for details.

#### build_variables=(\<array of assignments>)

_Valid modes: configure, makefile, scons_

An array used when redefining variables for the first execution of make

Example:

```fish
build_variables=(
   "DESTDIR=$target"
   "MANDIR=$target/man/man1"
)
```

#### install_variables=(\<array of assignments>)

_Valid modes: configure, makefile, scons_

Variables to be passed to `make install`. See `build_variables`.

#### make_variables=(\<array of assignments>)

_Valid modes: configure, makefile_

Variables to be passed to both `make` and `make install`. A shorthand to avoid
having to set everything twice, once in `build_variables` and then again in
`install_variables`.

#### makefile=\<makefile name>

_Valid modes: configure, makefile, xmkmf_

By default the makefile is assumed to be called `Makefile`. Use this variable to
override this value. See the note in `configure` for observations about
directory names given in variables of this kind.

Examples (only one applies at a time):

```fish
makefile=GNUmakefile
makefile=makefile
makefile=Makefile.linux
```

#### make=\<make command>

_Valid modes: configure, makefile, xmkmf_

By default the make command is assumed to be called `make`. This variable can be
used to override this value.

Example:

```fish
make=unsermake
```

#### build_target=\<make target>

_Valid modes: configure, makefile, xmkmf, python, scons_

The target to be used when calling make or equivalent build script/program to
build the program. More than one target may be given at a time, separating them
with spaces in a single declaration (you must use quotes).

Examples (only one applies at a time):

```fish
build_target=World
build_target="all shared"
```

#### install_target=\<make target>

_Valid modes: configure, makefile, xmkmf, python, scons_

The target to be used when calling make or equivalent build script/program to
build the program. More than one target may be given at a time, separating them
with spaces in a single declaration (you must use quotes).

Example:

```fish
install_target="install install.man install_shared"
```

#### do_build=no

_Valid modes: configure, makefile, python_

Compile should skip the `build` phase, and only do the `install` run. That is,
for Makefile-based recipes, it should run make only once.

#### do_install=no

_Valid modes: configure, makefile, xmkmf, python, scons_

Compile should skip the `install` phase, and only do the `build` run. That is,
for Makefile-based recipes, it should run make only once.

#### needs_build_directory=yes

_Valid modes: configure_

Some programs like Glibc recommend that a directory is created and used as a
working path during the execution of configure and make. Use of this variable is
transparent to other relative paths in other variables (such as `configure`),
but be aware that this special `build` directory will be active as a working
directory during the hook shell functions, instead of `dir`.

#### needs_safe_linking=yes

Deprecated

_Valid modes: all_

This option was used in older versions of the Scripts package to ensure that
some critical programs were symlinked into the `/System/Index` hierarchy in a
single step.

#### override_default_options=yes

_Valid modes: configure, python, scons_

Compile chooses some options by default according to the specified target type.
In configure recipes, it passes some standard autoconf options to the configure
script; in python recipes, distutils options for the Python build script; in
scons recipes, some standard options passed in invocations of scons.py. Use this
option to disable those options and have your own options (given in
configure_options or python_options) overwrite instead of append the option
list.

#### post_install_message="message"

_Valid modes: all_

A message to display to the user after installation.

#### sandbox_options=(\<array of options>)

_Valid modes: all_

Additional options to be passed to
[`SandboxInstall`]({{%relref "SandboxInstall" %}}). This is typically used to
expand the sandbox to allow additional directories in _special_ situations (such
as the installation of kernel modules). _Avoid_ using this option as much as
possible, and make sure you know what you're doing when you do use it.

Example:

```fish
sandbox_options=(
  "--no-sandbox"
)
```

#### symlink_options=(\<array of options>)

_Valid modes: all_

Additional options to be passed to
[`SymlinkProgram`]({{%relref "SymlinkProgram" %}}). This should be used sparingly,
in order to remedy unusual situations (the FreeType package used it to avoid a
XFree86 conflict which affected the proper functioning of the system). _Avoid_
using this option if possible; there are almost always better alternatives.

Example:

```fish
symlink_options=(
  "--conflict overwrite"
)
```

#### unmanaged_files=(\<files>)

_Valid modes: all_

Files to be installed in an unmanaged way to system locations such as
`/System/Variable.` One cannot install files under `/Programs` using this array.

Basically, unmanaged files are used to place files outside a program's $target
directory, and are to be used only when no real alternatives exist. That is, you
should not use this array to install files under `/usr` just because the
recipe's makefile define it as the default install location (this can be fixed
by changing the makefile variable defining it to $target).

Good examples of such files are kernel modules, which can't be linked but need
to be actually present under `/System/Kernel/Modules.`

#### with\_\<flag>

_Valid modes: cabal, cmake, configure, makefile, python, scons_

These are options to be appended to configure_options (or equivalent) in the
event that the use flag `flag` is set.

For instance,

```fish
with_gtk="--with-gtk=$gtk__path"
```

Or to add multiple configure options:

```fish
with_gtk=(
  "--with-gtk=$gtk_path"
  "--with-foo=$foo_path"
  "--with-bar=$bar_path"
)
```

See [Use flags]({{%relref "Use-flags" %}}).