---
title: "Advanced Topics"
weight: 1
---

## Patches

`Compile` has built-in support for applying patches distributed with recipes.
There are some things that should be considered when creating a patch for an
application. First of all, if the patch is generic, consider sending it
upstream, to the original project, as well. If that is done, here is how one
should do to get the patch working with `Compile`.

### Patch structure

`Compile` applies the patch from within the source directory with the `-p1`
option, stripping one directory from the patch's search path. This is to ensure
that the patch is appliable without editing even if the recipe is updated. The
patch should therefore add one level to the source directory in the path. An
example taken from the `rlocate` recipe, created with `diff`:

```diff
--- rlocate-0.4.3/doc/rlocate.html  2006-01-19 10:04:52.000000000 +0100
+++ rlocate-0.4.3.new/doc/rlocate.html  2006-01-19 19:10:20.000000000 +0100
@@ -223,6 +223,6 @@
```

Set the permissions of the rlocate and rlocated binaries. To do this execute the
following commands:

```diff
-        chown root:rlocate /usr/local/bin/rlocate
+        chown 0:rlocate /usr/local/bin/rlocate
         chmod 2755 /usr/local/bin/rlocate
```

This diff should then be in a file, say `01-root_to_uid.patch`, wich is placed
in the `Rlocate 0.4.3` recipe directory. Of course the filename should be
somewhat descriptive to what the patch does. The filename should also be
prefixed with a number, which ensures that the patches are applied in the
correct order, as there can be a number of patches, some of them being applied
to the same source file.

### Creating a patch

To create a patch you need the edited source and the "clean" source, then use
`diff` to create the patch. To create the patch in the example above I used

```fish
cd /Data/Compile/Sources
diff -Naur rlocate-0.4.3 rlocate-0.4.3.new > 01-root_to_uid.patch
```

where `rlocate-0.4.3.new` was the directory holding the edited source. This may
work if you only have one type of change made. But if you made several different
edits and want them in different patches one can specify the exact file to
'diff' or you can make a full diff and edit the resulting file, spliting it into
smaller patches.

### Converting patches

Perhaps there are already patches for the project, but they have the wrong path
in them. You can experience that the patches wont apply, even though they are
made for the specific application and version you are trying to `Compile`.
Either you can edit the patches and add or remove directories to the patch (more
precisely to the rows string with `+++` and `---`,
`--- rlocate-0.4.3/doc/rlocate.html 2006-01-19 10:04:52.000000000 +0100` in the
example above), so that there are exactly one directory above the source
directory. This can be tedious if it is a big patch. Then an easier way is to
apply the patch to the source and make a diff between the patched source and a
"clean" copy, just as when you create a new patch.

### Dynamic patches

Sometimes you want to add paths to the patches that are dependent on the host
system the application is installed on. Instead of adding the path statically to
the patch `Compile` has support for dynamically created patches. By placing the
suffix `.in`, e.g. `01-root_to_uid.patch.in`, on the patch you tell `Compile`
that it should parse the file and generate the patch `01-root_to_uid.patch`,
with certain strings replaced with values dependant on the system. The same
[variables used in
recipes]({{%relref "Recipe-Format-Specification#dynamic-variables" %}}) can be used
in patches but prefixed with the string `Compile_` and padded with `@%` and
`%@`. So, for example, if `rlocate` depended on the application `foo`, the
variable used in recipes to reference `foo`'s installation directory would be
`$foo_path` and therefore the string used in patches to reference this path
would be `@%Compile_foo_path%@`. Below are valid variables for target
application as well as directories belonging to the dependency `foo`:

-   `@%Compile_target%@`
-   `@%Compile_settings_target%@`
-   `@%Compile_variable_target%@`
-   `@%Compile_foo_path%@`
-   `@%Compile_foo_settings_path%@`
-   `@%Compile_foo_variable_path%@`

## Binary recipes

Full article: [Binary recipes]({{%relref "Binary-Recipes" %}})

Binary recipes are used to install vendor-supplied precompiled binaries of
software. They are usually created using the manifest recipe type, and have
`_bin` suffixed to their version.

## Recipe types

See also: [Recipe types reference]({{%relref recipe-types %}})

The `Compile` tool can handle numerous types of packages, each of them with a
different build technique.

When [`MakeRecipe`]({{%relref "MakeRecipe" %}}) is invoked, it downloads the
program's source, uncompresses it and tries to detect what kind of build system
it uses. And, surely, there are some packages on which
[`MakeRecipe`]({{%relref "MakeRecipe" %}}) cannot detect that. This is when the
user's interaction is needed, and some manual modifications on the Recipe must
be done.

As presented in the [`Compile`]({{%relref "Compile" %}}) section, `Compile` handles
compilation of programs according to a few number of "recipe types". For each
type, there are valid declarations that you can specify, to adapt the behavior
of `Compile` to the needs of the program that is about to be compiled. The full
list of declarations is at Appendix "[Recipe format
specification]({{%relref "Recipe-Format-Specification" %}})". Let's see some of the
main options for each type:

### configure recipes

These are **autoconf**-based packages, and are indicated with
`recipe_type=configure`. The most common variation in recipes of this type is
the need to pass additional flags to the `configure` script. You can do so with
the `configure_options` flag, like this:

```fish
configure_options=(
    "--enable-shared"
    "--with-foo"
)
```

Keep in mind that by passing explicit flags to **configure**, you are affecting
the dependencies of the package. Ideally, the **configure** script should be
able to detect what's available in the system and enable or disable features.
Much progress in this area has been made in the last few years, especially with
[`Pkgconfig`](http://pkgconfig.freedesktop.org), but still some programs require
flags to be passed explicitly.

In **configure**-based recipes, `Compile` uses
[`PrepareProgram`]({{%relref "PrepareProgram" %}}) to detect if some standard
parameters such as `--prefix` are supported by the configure script. If the
program does not support these parameters and
[`PrepareProgram`]({{%relref "PrepareProgram" %}}) detects them incorrectly, you
can use `override_default_options=yes` to have `configure` use _only_ the
options given by you in `configure_options`.

Another occasionally necessary flag is `autogen_before_configure=yes`. Some
programs distribute the necessary input files for generating `configure` (such
as `configure.ac` or `configure.in`) but do not ship the generated script, only
a builder script `autogen.sh`. Using this flag, `autogen.sh` will be executed as
a first step.

If **configure** or **autogen.sh** have non-standard names, you can explicitly
provide them with `configure` and `autogen`, like this:

```fish
configure=configure.gnu
autogen=gen_all.sh
```

If present at `<architecture>/Recipe`, an architecture-specific Recipe file is
sourced in addition to the base Recipe file. Variable assignments in it will
override earlier ones, so to append to a variable, you must do so explicitly,
e.g.

```shell
configure_options=(
    "${configure_options[@]}"
    --with-cpu=i686
    --enable-add-ons
)
```

Since "compileprogram" recipes also run `make`, most of the observations about
"makefile" recipes, discussed below also apply.

### makefile recipes

These are packages that use **Makefiles** directly. You can easily spot programs
of these type: when the program's installation instructions just tell you to run
`make` from command line without a previous step, they are recipes of this kind.

For this kind of recipe, `Compile` runs `make` twice: the "build" run and the
"install" run. A few programs require only one run; you can disable either with
`do_build=no` and `do_install=no`.

In "makefile" recipes, you will always have to pass at least one additional
option in the recipe, to tell the Makefile to use the
`/Programs/program-name>/version>` directory. If we're lucky, the Makefile has
one main variable that controls the installation prefix. Variables of this kind
are usually called `PREFIX`, `DESTDIR`, `INSTDIR`... you'll have to look inside
the `Makefile` to find out. Remember that the installation prefix is set by
`Compile` as the `$target` shell variable. To give `make` variables, we can
either use `build_variables` and `install_variables`, which give options to the
"build" and "install" runs of `make`, or just `make_variables` which passes
options to both runs. Their use is similar to that of `configure_options`.

```fish
make_variables=(
    "DESTDIR=$target"
)
```

Sometimes, paths are defined in several variables of the `Makefile`. No problem:

```fish
make_variables=(
    "BINDIR=$target/bin"
    "LIBDIR=$target/lib"
    "ETCDIR=$target/../Settings"
)
```

If there are no variables of this kind in the `Makefile`, that is, if the
`Makefile` has hard-coded locations in its installation rules, then
unfortunately you'll have to patch the `Makefile` (and possibly the source code,
look for references to paths like `/usr` using `grep`).

Like with `configure` and `autogen`, if the makefile uses a different name from
the standard (`Makefile`), you can pass it explicitly using the `makefile`
variable:

```fish
makefile=GNUmakefile
```

### python recipes

The "python" recipe type is used for programs using Python Distutils as a build
system. Since it is so recent, there is a number of minor variations floating
around (some packages use `setup.py`, others use `build.py`, etc.) -- "python"
tries to detect these variations where possible, but ultimately there are flags
to specify special cases explicitly.

The name of the build script can be given with `build_script`. You can control
the two runs of the Python build script using the same options as "makefile
recipes" (`do_build=no` and `do_install=no` to disable runs, `build_target` and
`install_target` to name the runs). Custom options can be passed with
`python_options`. Again, `override_default_options=yes` can be passed to skip
auto-detected flags if needed.

### xmkmf recipes

This is for recipes based on the old "xmkmf -->--> imake" system historically
used by the X Window System. This is being phased out in Xorg 7.0 in favor of
GNU autoconf.

### scons recipes

This is for recipes based on SCons.

### manifest recipes

"Manifest" recipes are used for programs that just need to copy files over. The
`manifest` array-style entry lists colon-separated pairs, indicating source file
and target destination, relative to `target`. (See "[Recipe format
specification]({{%relref "Recipe-Format-Specification" %}})" for details).
