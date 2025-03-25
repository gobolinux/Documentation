---
title: "Use Flags"
weight: 8
---

Use Flags are a way to affect the compilation of a [Recipe](/Recipes) based on
the Programs installed on a system and the user's preferences, without having to
edit the Recipe explicitly. Different configure options may be passed to the
program being compiled, and additional hook functions may be run by Compile,
depending on which flags are activated. Flags may be activated by the presence
of installed dependencies, or explicitly by the user.

Also see [Available use flags](Available-Use-Flags).

## Use Flags Names

Flags are lower-case alphanumeric plus underscore, and should be named after
what they do - the other program, tool, hardware, or functionality they enable,
with any other characters stripped out if necessary.

Example names would be `python`, `ipw2200`, `gtk`.

## Enabling Use Flags

Flags are enabled in three ways. The first is through the global default flag
set, in `/Programs/Scripts/Current/Data/SystemUseFlags.conf`. At the moment,
this set is empty, but it will probably end up populated based on what is used
for packages and the ISO. The second is the local flags, set in
`/System/Settings/UseFlags.conf`. Finally, the `USE` environment variable is
read for flag specifications. It is intended that this be used for single
Compile runs, such as for testing recipes, and not to set flags for your system
(use `UseFlags.conf` for that). Later flag specifications overwrite earlier
ones, both in the order listed above and within the files.

A flag specification has the format `(-|+)<flag>[ program1[ program2 ...]]`. `+`
enables the flag, `-` disables it, and providing a space-separated list of
programs after the flag makes that specification apply only to those programs.
Only one flag specification should be included on each line, and everything
after a `#` is ignored as a comment. An example file for clarity:

```diff
+foo # Enable foo globally. This text is ignored.
-bar
+bar FooBar
```

This enables the foo flag globally and disables bar, but then enables the bar
flag for only the program `FooBar`. If the last two lines were the other way
around, bar would be globally disabled again. A special specification is -\*.
This disables all flags, and is probably most useful in the environment
variable.

The environment variable takes a space-separated list of flag specifications
(rather than newline), so it accepts a special syntax for the specifications,
with `@` instead of a space when listing programs to go with a flag. It takes
the ugly syntax because it's likely to be by far the least common way of using
it. The same set of flags from above could be applied with:

```fish
USE="+foo -bar +bar@FooBar"
```

## Use Flags in Recipes

Flags should be listed in the
[Dependencies]({{%relref "Recipe-Format-Specification#dependencies" %}}) or
[BuildDependencies]({{%relref "Recipe-Format-Specification#builddependencies" %}})
file in the same manner as the existing cross/!cross flag:

```fish
FooBar >= 1.2 [foo,bar]
```

Flags are separated by commas, and treated as a disjunction - the dependency
will be enabled if and only if at least one of the listed flags is enabled. If
the `cross`/`!cross` flag is specified, it must be the first flag listed
(technical limitation; may be lifted in time).

If a flag has no associated dependency, first consider whether it is necessary
at all, or whether support should just be enabled by default. If the flag is
necessary, it should be listed at the end of the Dependencies file as an entry
without a corresponding dependency:

```fish
FooBar >= 1.2 [foo,bar]
[baz,quux]
```

Dependency-free flags may be necessary when associated with hardware, or when
there is some lengthy compilation, large filesize, or mutual incompatibility
associated with them.

Within a Recipe file, the `with_<flag>` variable may be set for the common case
of adding a `configure` option:

```fish
with_gtk="--with-gtk=$gtk__path"
```

Or to add multiple `configure` options:

```fish
with_gtk=(
    "--with-gtk=$gtk_path"
    "--with-foo=$foo_path"
    "--with-bar=$bar_path"
)
```

This will add the value of the variables to the most common configuration array
for the recipe type. For `configure`, this is `configure_options`; Other options
are: `python`, `python_options`; `makefile`, `build_variables`; `scons`,
`scons_variables`; cmake, `cmake_options`; `cabal`, `cabal_options`. In the case
where more complicated changes are needed to enable support, there is a function
`using_<flag>()` available:

```fish
using_gtk() {
   configure_options=( "${configure_options[@]}" "--with-gtk=$gtk__path" )
}
```

This example does the same thing as the `with_gtk` one above, but the function
can alter other variables as well. It should not alter code, execute scripts,
move files, or apply patches; that is what the flag hook functions are for. Each
of the existing hook functions (`pre_link`, `pre_patch`, `pre_build`,
`pre_install`, `post_install`) has a corresponding `using_<flag>_<hook>()`
function:

```fish
using_gtk_pre_build() {
   rm -rf *
}
```

These are run through `Run_Hook` and so are sudoed the same as the bare hooks
(for the moment). This may cause problems if you create files or directories
from the hook, so keep it in mind (it applies to all hook functions, but it
should be noted especially too). If necessary, you can unsudo yourself with
`exec sudo -u "$SUDO_USER" -H env SUDO_OK=1 $0 "${@}"`. That won't affect
anything other than the currently-executing hook, so it should be safe.

In most cases, dependencies are autodetected by configure correctly and no
change to the Recipe file will be necessary. In that case, the `with_<flag>`
variables should _not_ be used only to convey redundant information, and the
flag should just be listed appropriately in Dependencies. Note that this means
that unlike Gentoo's, our flags are not exclusive: their support may be compiled
in even if the flag is disabled, if the dependency is installed and autodetected
correctly. Compilations using ChrootCompile will not experience this effect, as
the dependency will be left out of the chroot environment.

This means that in the ideal world of well-behaved software, the `Recipe` file
itself should need no modification at all. Complex or less well-behaved software
will inevitably end up with longer and more complicated recipes, but in most
cases they should be concise and simple.

In all cases, only the variables and functions for flags that are both enabled
and listed in the `(Build)?Dependencies` file will be applied, and others have
no effect even if the flag is enabled. This avoids looping through many
inapplicable flags several times during the Compile process.

The flags enabled for a given compilation are saved into `Resources/UseFlags` in
the installed program directory. This enables tools such as Freshen to display
which flags have changed state since the last installation of a given program,
or find programs that could benefit from recompilation.

## Use Flags in Tools Development

Flags are accessed from the shell through the `UseFlags` script, which takes
either a program name or a recipe directory as its first argument. The latter
method is preferred where possible, because it will read the Dependencies file
and limit the flags to only those listed there; giving just a name will include
all flags that would be enabled for that program (including global flags that it
doesn't use at all). With only one argument, it will output the list of flags to
standard output, one per line, suitable for iterating in a script or saving to a
file. If called with no arguments, it will do the same for only global flags.

Given a second argument of a flag to test, the script returns true if the flag
is enabled, and false otherwise. If the `-v` option is specified, it will also
output a message giving the state of the flag.

From Python, the module is named `UseFlags` and may be imported as usual. The
most important method is `UseFlags`, which takes an (optional) program
parameter, which can also be either a recipe directory or a program name. It
returns a frozenset of the enabled flags. The return value is cached, so the
method may be called repeatedly with the same arguments without much penalty.
Another useful public method is `potentialFlags`, which takes _only_ a recipe
directory and returns a frozenset of all the flags that could possibly be
enabled for that recipe. Freshen uses that to provide output on which flags
could be enabled, modeled after emerge, only without the ugliness. The other
methods should be treated as private.

See the
[mailing list thread](http://thread.gmane.org/gmane.linux.distributions.gobo.devel/2593).
