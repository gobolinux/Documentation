# Recipe Format Specification

This is the official specification document for the GoboLinux recipe format.

The term "Recipe" can refer to either:
* A packed recipe, as held in GoboLinux recipe store, with a name like `Foo--1.0-r1--recipe.tar.bz2`.
* The file `Foo/1.0-r1/Recipe` in such a tarball. This is also called the "recipe file".

## File Layout

A packed recipe is a tarball such as `SomeProgram--Version-r1--recipe.tar.bz2`
with the following directory structure. 

```
SomeProgram/
   `--Version-r1/
        |-- Recipe               (required)
        |-- *.patch                  
        |-- *.patch.in               
        |-- Resources/
        |     |-- Dependencies   (required)
        |     |-- Description    (required)
        |     |-- Defaults/          
        |     |     |-- Settings/
        |     |     `-- Variable/
        |     |
        |     |-- Tasks/             
        |     |-- Wrappers/          
        |     |-- BuildDependencies  
        |     |-- BuildInformation   
        |     |-- Environment        
        |     |-- Hints              
        |     |-- PostInstall        
        |     `-- Requirements       
        |     
        `-- <arch>/                  
              |-- Recipe
              `-- Resources/
```

where `<arch>` represents one or more optional architecture directories named
`i686/`, `x86_64/`, `arm/`, `ppc/`, etc.

# The Recipe file

The Recipe file contains a series of directives using shell assignment
and shell function syntax. Supported directives presented below, divided
into categories:

* [Getting the source](#getting-the-source) - tells Compile how to fetch
  the software
* [Recipe types](#recipe-types) - tells Compile which tactic to use to
  compile the software
* [Other directives](#other-directives) - further customize the compilation
  process.
  
A minimal recipe will have at least two directives, one specifying how to get
the source (such as `url`) and `recipe_type` to tell what is the method to use
when building it.

## Getting the Source 

Source archives may be downloaded from static urls or from various version
control systems. In the case of a static url, a size and md5sum should be
included for verification. The following Recipe options control this phase. 
All these options are valid for all recipe types.

### Static URLs 

#### url=&lt;url&gt; 

Note: For Sourceforge URLs, use the variable $httpSourceforge, as in

```
 url=$httpSourceforge/&lt;project name&gt;/&lt;filename&gt;
```

e.g.

```
 url=$httpSourceforge/xmule/xmule-1.8.2.tar.bz2
```

Similarly, use `$ftpGnu`, and `$ftpAlphaGnu`, for downloads from GNU's ftp servers.

#### urls=(&lt;array of urls&gt;) 

If the Program has multiple source packages, you may specify a list of them.
If a partial file exists, resumption is
attempted. FTP transfers are always performed in passive mode.

#### mirror_url=&lt;url&gt; 

#### mirror_urls=(&lt;array of urls&gt;) 

URLs to be used, in case the URLs listed in `url`/`urls` fail.
Multiple mirrors may be specified. For sets of URLs, each mirror
needs to specify the same number of URLs.

Example:

```
urls=(
   "http://www.main-site.org/file1"
   "http://www.main-site.org/file2"
)
mirror_urls=(
   "http://www.mirror1.org/file1"
   "http://www.mirror1.org/file2"
   "http://www.mirror2.org/file1"
   "http://www.mirror2.org/file2"
)
```

#### file=&lt;filename&gt; 


#### files=(&lt;array of filenames&gt;) 

The name of the package file containing the program's sources.
If not specified, it is assumed to be the same as the final part
of the URL, after the last slash.
If `urls` is used instead of `url`, `files` is expected to
contain the same number of entries as `urls`. All of them are
unpacked relative to the same directory by default.  To change this
behaviour see [unpack_files](#unpack_files) below.


#### file_size=&lt;size&gt; 


#### file_sizes=(&lt;array of sizes&gt;) 

This is the file size(s), in bytes, of the packed archive(s) (e.g. foo.tar.gz)
as reported by `ls -l`.

```
user@gobo /Files/Compile/Archives]ls -l gettext-0.16.1.tar.gz
-rw-r--r-- 1 root root 8539634 Jul 11 01:08 gettext-0.16.1.tar.gz
```

#### file_md5=&lt;md5sum&gt; 


#### file_md5s=(&lt;array of md5sums&gt;) 

This value contains the [MD5Sum](http://en.wikipedia.org/wiki/MD5) of the
package file defined by the `file` value. You can find
this MD5Sum by using the `md5sum` command.

```
user@gobo /Files/Compile/Archives]md5sum gettext-0.16.1.tar.gz
3d9ad24301c6d6b17ec30704a13fe127  gettext-0.16.1.tar.gz
```

### Version Control Systems 


#### cvs=&lt;CVS server&gt; 


#### cvss=(&lt;array of CVS servers&gt;) 

Specify the CVS server and repository to be used. Note that
`cvs`, `svn` and `url` are mutually exclusive, since you should be either
fetching from SCM or getting a tarball.

Example:

```
cvs=:pserver:anonymous:@anoncvs.gimp.org:/cvs/gnome
```

#### cvs_module=&lt;module name to checkout&gt; 


#### cvs_modules=(&lt;array of module names to checkout&gt;) 

CVS module to be checked out.

Example:

```
cvs_module=gimp
```

#### cvs_opts=&lt;string added to cvs operation&gt; 


#### cvs_options=&lt;string added to cvs operation&gt; 

Some server configurations require additional options to be
passed to the cvs command. You shouldn't normally
need this command, but it is available in case the documentation
of the project you're checking out instructs you to give special
options to cvs.

`cvs_options` is a synonym to `cvs_opts`.


#### cvs_password=&lt;password&gt; 

Password to log into the cvs server.


#### cvs_checkout_options=&lt;string added to cvs checkout operation&gt; 

Some configurations require additional options to be passed
specifically to the cvs checkout command, such as for getting
a snapshot from a specific date. Normally, you shouldn't need this command.


#### cvs_rsh=&lt;string&gt; 

Specify a value for the CVS_RSH variable (see cvs documentation
for details). If unset, `ssh` is used by default.


#### svn=&lt;SVN server&gt; 


#### svns=(&lt;array of SVN servers&gt;) 

Specify the Subversion server and repository to be used. Note that
`cvs`, `svn` and `url` are mutually exclusive, since you should be either
fetching from a SCM or getting a tarball.

Example:

```
svn=http://svn.apache.org/repos/asf/httpd/httpd/branches/2.2.x
```

#### bzr=&lt;bazaar server&gt; 


#### bzrs=(&lt;array of bazaar servers&gt;) 



#### git=&lt;git server&gt; 


#### gits=(&lt;array of git servers&gt;) 


#### hg=&lt;mercurial server&gt; 


#### hgs=(&lt;array of mercurial servers&gt;) 

Similarly, specify an URL for checkout from a Bazaar, Git, or Mercurial
server, respectively.


## Recipe types 

Supported recipe types (also known as modes), to be given as argument to
`recipe_type`:


### configure 

`recipe_type=configure` is used for Programs based on `configure` scripts,
(autoconf or not.) Some options are only relevant for *configure*:


#### configure_options=(<array of options>) 

Flags to be passed to the configure script. These flags are
passed in addition to default flags detected by [[PrepareProgram]]
(such as --prefix and --sysconfdir on autoconf-based configure
scripts), unless the override_default_options declaration is used.


#### autogen_before_configure=yes 

Use it if you need to run `./autogen.sh` in order to generate the configure
script.


#### autogen 

The program to run for the above.  Defaults to `autogen.sh`.


#### configure=<program name> 

By default the configure script is assumed to be called
`configure`. Use this variable to override this value.
Remember that the current directory during execution
will still be the one set by the `dir` variable, even if a
directory path is given (as in the second example below).
If the behavior you intended is for Compile to `cd` to the `unix`
directory and run its build sequence there, use `dir` instead.

Examples (only one applies at a time):
```
 configure=Configure.gnu
 configure=unix/configure
```

### cabal 

`recipe_type=cabal` is used for Programs based on Cabal, the
package manager for Haskell.
Some options are only relevant for *cabal*:


#### cabal_options=(<array of options>) 

Flags to be passed to the Cabal configure operation.

These flags are passed in addition to default flags detected by
[[PrepareProgram]] (such as --prefix) unless the override_default_options
declaration is used.


#### runhaskell 

Specifies the method of invoking Haskell to perform a Cabal-based compilation.
 The default is `runhaskell`.


### cmake 

`recipe_type=cmake` is used for Programs based on CMake.
Some options are only relevant for *cmake*:


#### cmake_options=(<array of options>) 

Flags to be passed to the CMake configure operation.
These flags are passed in addition to default flags (such as -DCMAKE_INSTALL_PREFIX).


#### cmake_variables=(<array of assignments>) 

Variables to be defined in the environment during the execution of *cmake*.


### makefile 

`recipe_type=makefile` is used for Programs based on Makefiles.
No options are relevant only for *makefile*.


### python 

`recipe_type=python` is used for Programs based on Python Distutils.
Some options are only relevant for *python*:


#### python_options=(<array of options>) 

Array of options to be passed to the Python Distutils build script.
This works similarly to the `configure_options` array.


#### build_script=<name> 

Specify the same for the Python build script. If none
is given, Compile tries a few default ones, such as setup.py.


### scons 

`recipe_type=scons` is used for Programs based on SCons.
Some options are only relevant for *scons*:


#### scons_variables=(<array of assignments>) 

Variables to be passed to *scons*.


### xmkmf 

`recipe_type=xmkmf` is used for Programs based on X11 Imake.
No options are relevant only for *xmkmf*.


### manifest 

`recipe_type=manifest` is used to directly copy appropriate files from the
archive into place. Some options are only relevant for *manifest*:


#### manifest=(<array of "file:dir">) 

Specify which files should be copied over, and to where.
Destination is relative to `target`.

Example:

```
manifest=(
   "some_script:bin"
   "include/a_header.h:include"
   "lib/libfoo.so:lib"
)
```

### meta 

`recipe_type=meta` only depends on other Recipes.
All included recipes are built relative to the same installation prefix.
Some options are only relevant for *meta*:


#### include=(<array of recipes>) 

In a meta-recipe, this array holds the list of recipes that should
be built to constitute the complete program. Recipe names should
be in the format `App--1.0`. The order of the entries in the
array is significant, because it is the order in which the recipes
are built. Note: be careful with the order, because re-building
a meta-package that's already installed may cover up ordering
problems.


#### part_of=<parent> 

Indicates that this recipe is generally included as part of a meta-recipe. 
Unless Compile is called with `-i`/`--install-separately`, the Program will be
installed into the parent Program's directory. Implies `keep_existing_target`.


#### update_each_settings=yes 

In meta-recipes, Compile only calls UpdateSettings for the meta-recipe and not
for its sub-recipes. Set this variable to override this behavior and have
UpdateSettings called in every sub-recipe.


## Other directives 

#### compile_version=<version-number> 

*Valid modes: all*

The version number of Compile used to create this recipe.


#### environment=(<array of variables>) 

*Valid modes: all*

Environment variables to be applied to the shell where the compilation takes
place. Each entry of the array must be in the format `variable=value`.

Example:

```
environment=(
   "PYTHONOPTIMIZE=2"
)
```

#### uncompress=no 

*Valid modes: all*

Used for urls where the files are going to be used directly. Not a common option.


#### unpack_files 

*Valid modes: all*

*Possible values:* `inside_first, contents_inside_first, dirs, files_in_root`.

Relevant when `files=(more than one file to download)` is used, or when a
single archive has "loose files" without an enclosing directory.

By default, all entries in `files` are unpacked in the same
directory. This flag can be used to override this behavior.
`inside_first` tells it to unpack `files[0]` and then unpack
all subsequent files inside the resulting directory.

`contents_inside_first` tells it to unpack `files[0]`, then unpack the
remaining files, and move the contents of the resulting unpacked `dirs` into
the first directory.

`dirs` tells it to use the directories explicitly specified in
the `dirs` array as destinations for each file.

For example, if `files` is (foo.tar.gz bar.tar.gz) and
foo.tar.gz contains

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

Using `dirs`, virtually any path structure can be used. Since
the first entry in the `dirs` array is special, it is not used
by `unpack_files`.
If any of the `dirs` entries contains the value of the `target`
array, the `keep_existing_target` is implied (it can still be
explicitly overridden in the recipe, but then the user might
delete the data that was just unpacked).

Using `files_in_root`, Compile assumes files are stored in the
archive without a directory. A directory is created so that
files are unpacked inside it, avoiding scattering files in
$compileSourcesDir (typically `/Data/Compile/Sources`).


#### dir=<directory> 


#### dirs=(<array of directories>) 

*Valid modes: all*

Indicates the directory to `cd` into after the package is unpacked.
If not specified, the name of the package file (stripped of its
extension) is assumed.
If `dirs` is used instead of `dir`, `dirs` is expected to
contain the same number of entries as `urls`.
The first entry in the array is special: the compilation method
is applied only on the first directory. To compile multiple packages
into a single program, use meta-packages (`is_meta`).
The usage of `dirs` affects the way files are unpacked. See
`unpack_files` for details.


#### docs=(<array of filenames>) 

*Valid modes: all*

A list of filenames, relative to the program's sources root,
of files to be copied to the program's `doc/` dir (or `doc/$app/`
for meta-packages).  Wildcards are supported but must be
single-quoted. Note that some default names such as README*,
AUTHORS and TODO are automatically fetched.

Example:

```
docs=(
   'docs/*.html'
)
```

#### create_dirs_first=yes 

*Valid modes: configure, makefile*

By default, Compile only generates directories in the target location
right before the installation step. This is useful for the --no-install
option (see the [[Compile]] reference entry). Unfortunately, some
programs fail during the configuration of compilation step if the
target directory does not already exist. Use this entry to appease those
programs.


#### keep_existing_target=yes 

*Valid modes: all*

When set, it will not ask the user if they want to erase the
contents of the $target (if any) prior to compiling the program.
This is implicitly set if the `dirs` array contains any reference
to `target`. See `unpack_files` for details.


#### build_variables=(<array of assignments>) 

*Valid modes: configure, makefile, scons*

An array used when redefining variables for the first execution
of make

Example:

```
build_variables=(
   "DESTDIR=$target"
   "MANDIR=$target/man/man1"
)
```

#### install_variables=(<array of assignments>) 

*Valid modes: configure, makefile, scons*

Variables to be passed to `make install`. See `build_variables`.


#### make_variables=(<array of assignments>) 

*Valid modes: configure, makefile*

Variables to be passed to both `make` and `make install`.
A shorthand to avoid having to set everything twice, once
in `build_variables` and then again in `install_variables`.


#### makefile=<makefile name> 

*Valid modes: configure, makefile, xmkmf*

By default the makefile is assumed to be called
`Makefile`. Use this variable to override this value.
See the note in `configure` for observations about
directory names given in variables of this kind.

Examples (only one applies at a time):

```
 makefile=GNUmakefile
 makefile=makefile
 makefile=Makefile.linux
```

#### make=<make command> 

*Valid modes: configure, makefile, xmkmf*

By default the make command is assumed to be called `make`.
This variable can be used to override this value.

Example:

```
make=unsermake
```

#### build_target=<make target> 

*Valid modes: configure, makefile, xmkmf, python, scons*

The target to be used when calling make or equivalent build
script/program to build the program. More than one target
may be given at a time, separating them with spaces in
a single declaration (you must use quotes).

Examples (only one applies at a time):

```
 build_target=World
 build_target="all shared"
```

#### install_target=<make target> 

*Valid modes: configure, makefile, xmkmf, python, scons*

The target to be used when calling make or equivalent build
script/program to build the program. More than one target
may be given at a time, separating them with spaces in
a single declaration (you must use quotes).

Example:

```
install_target="install install.man install_shared"
```

#### do_build=no 

*Valid modes: configure, makefile, python*

Compile should skip the `build` phase, and only
do the `install` run. That is, for Makefile-based recipes,
it should run make only once.


#### do_install=no 

*Valid modes: configure, makefile, xmkmf, python, scons*

Compile should skip the `install` phase, and only
do the `build` run. That is, for Makefile-based recipes,
it should run make only once.


#### needs_build_directory=yes 

*Valid modes: configure*

Some programs like Glibc recommend that a directory is
created and used as a working path during the execution of
configure and make. Use of this variable is transparent
to other relative paths in other variables (such as `configure`),
but be aware that this special `build` directory will be active
as a working directory during the hook shell functions, instead
of `dir`.


#### needs_safe_linking=yes 

Deprecated

*Valid modes: all*

This option was used in older versions of the Scripts package
to ensure that some critical programs were symlinked into
the `/System/Index` hierarchy in a single step.


#### override_default_options=yes 

*Valid modes: configure, python, scons*

Compile chooses some options by default according to
the specified target type. In configure recipes, it
passes some standard autoconf options to the configure script;
in python recipes, distutils options for the Python build script;
in scons recipes, some standard options passed in invocations
of scons.py.
Use this option to disable those options and have your own
options (given in configure_options or python_options) overwrite
instead of append the option list.


#### post_install_message="message" 

*Valid modes: all*

A message to display to the user after installation.


#### sandbox_options=(<array of options>) 

*Valid modes: all*

Additional options to be passed to [[SandboxInstall]]. This
is typically used to expand the sandbox to allow additional
directories in *special* situations (such as the installation
of kernel modules). *Avoid* using this option as much as
possible, and make sure you know what you're doing when
you do use it.

Example:

```
sandbox_options=(
  "--no-sandbox"
)
```

#### symlink_options=(<array of options>) 

*Valid modes: all*

Additional options to be passed to [[SymlinkProgram]]. This
should be used sparingly, in order to remedy unusual situations
(the FreeType package used it to avoid a XFree86 conflict which
affected the proper functioning of the system). *Avoid* using
this option if possible; there are almost always better alternatives.

Example:

```
symlink_options=(
  "--conflict overwrite"
)
```

#### unmanaged_files=(<files>) 

*Valid modes: all*

Files to be installed in an unmanaged way to system locations such as
`/System/Variable.` One cannot install files under `/Programs` using this array.

Basically, unmanaged files are used to place files outside a program's $target
directory, and are to be used only when no real alternatives exist. That is,
you should not use this array to install files under `/usr` just because the
recipe's makefile define it as the default install location (this can be fixed
by changing the makefile variable defining it to $target).

Good examples of such files are kernel modules, which can't be linked but need
to be actually present under `/System/Kernel/Modules.`


#### with_<flag> 

*Valid modes: cabal, cmake, configure, makefile, python, scons*

These are options to be appended to configure_options (or equivalent) in the
event that the use flag `flag` is set.

For instance,
```
 with_gtk="--with-gtk=$gtk__path"
```

Or to add multiple configure options:
```
 with_gtk=(
    "--with-gtk=$gtk_path"
    "--with-foo=$foo_path"
    "--with-bar=$bar_path"
 )
```

See [[Use flags]].


## Hooks 

Besides the declarative variables, recipes can also contain imperative
commands, in the form of bash shell functions. This is the order the functions
are called for each recipe type:

Note: pre_patch will not be called if there are no patches.


#### configure: 

* `pre_patch()`
* patch, if any
* `pre_build()`
* configure
* make
* `pre_install()`
* make install
* `pre_link()`
* symlink
* `post_install()`


#### cabal: 

* `pre_patch()`
* patch, if any
* cabal configure (affected by `$runhaskell` and `$cabal_options`)
* `pre_build()`
* cabal build (affected by `$runhaskell`)
* `pre_install()`
* cabal install (affected by `$runhaskell`)
* symlink
* `post_install()`


#### makefile: 

* `pre_patch()`
* patch, if any
* `pre_build()`
* make
* `pre_install()`
* make install
* `pre_link()`
* symlink
* `post_install()`


#### manifest: 

* `pre_patch()`
* patch, if any
* `pre_install()`
* copy files
* `pre_link()`
* symlink
* `post_install()`


#### python: 

* `pre_patch()`
* patch, if any
* `pre_build()`
* python setup.py build
* `pre_install()`
* python setup.py install
* `pre_link()`
* symlink
* `post_install()`


#### scons: 

* `pre_patch()`
* patch, if any
* `pre_build()`
* scons.py
* `pre_install()`
* scons.py install
* `pre_link()`
* symlink
* `post_install()`


#### xmkmf: 

* `pre_patch()`
* patch, if any
* `pre_build()`
* xmkmf
* make
* `pre_install()`
* make install
* `pre_link()`
* symlink
* `post_install()`


### Private shell functions 

For shell functionality to be shared, for example between sub-recipes of
different architectures, it is possible to define additional shell functions
in the recipe. Their names must be prefixed with `private__`.

### Use flag hooks 

Additional shell functions `using_<flag>()` will be run for each use flag
`flag` which is set. Do not do anything in such a function which depends on
time of execution.  Instead, use `using_<flag>_<hook>()`.  For instance,
`using_gtk_pre_build()` is run at the time specified above, in the event that
the `gtk` use flag is set.

See [[Use flags]].


### New Hooks 


Since version 1.12.0, Compile supports a new set of hooks. These hooks can be
used to override any of the steps in the compilation process, and are
available to all recipe types. As with the "old" hooks discussed above, the
new hooks shouldn't be necessary for most recipe types, but they are useful
for cases in which the compilation process needs to perform nonstandard steps.

In order of invocation, these are the new hooks:

* `do_fetch()`
* `do_unpack()`
* `do_patch()`
* `do_configuration()`
* `do_build()`
* `do_install()`

If any of these hooks are defined in your recipe, Compile will call it instead
of performing the standard corresponding step for the recipe type you are
using. So, for instance, if your recipe needs to perform the installation step
in some nonstandard way, your recipe should include something like this:

```
  do_install() {
    # ... your code for nonstandard installation goes here ...
  }
```

Notice that this will *not* perform the standard configuration steps. If you
need to perform some nonstandard steps *in addition to* the standard steps,
you can call the default Compile functions from your own hook. The function
that performs the default installation step for recipes of type manifest, for
instance, is called `manifest_do_install()`. Using it would look like
this:

```
  do_install() {
    # Perform the regular installation (for recipes with manifest type)
    manifest_do_install "$@"
    
    # Perform some additional, nonstandard steps
    # ... some ...
    # ... nonstandard ...
    # ... installation ...
    # ... steps ...
    # ... here ...
  }
```

## Dynamic variables 


Compile automatically creates variables that can be used in the functions.


### System variables 

To help you in recipe writing, Compile gives you the following run-time
variables to use, each referring to a specific filesystem hierarchy's member.

* `$goboExecutables`
* `$goboHeaders`
* `$goboModules`
* `$goboLibraries`
* `$goboPrograms`
* `$goboSettings`
* `$goboTemp`
* `$goboVariable`

Which respectively point to (by default):

* `/System/Index/bin`
* `/System/Index/include`
* `/System/Kernel/Modules`
* `/System/Index/lib`
* `/Programs`
* `/System/Settings`
* `/System/Variable/tmp`
* `/System/Variable`

Thus, if you're writing a recipe for some program which accepts configure
options and for which you need to manually specify a library path, you can use
the $goboLibraries variable like

```
 configure_options=(
    "--with-extra-libraries=$goboLibraries/<path_to_the_library>"
 )
```

The same applies to the remaining as well, depending on specific program's needs.


### Program variables 

For every recipe there will always be variables for the program prefix as well
as variables for the settings directory and the variable directory for the
program.

* `$target`
* `$settings_target`
* `$variable_target`

For the recipe for `Foobar 2.1` those variables will have the values of
`$goboPrograms/<nowiki>FooBar</nowiki>/2.1`,
`$goboPrograms/<nowiki>FooBar</nowiki>/Settings` and
`$goboPrograms/<nowiki>FooBar</nowiki>/<b></b>Variable` respectively.


### Dependency variables 

There will also be variables for every dependency listed in the Dependency
file. If for example `Foo 1.2` is listed as dependency, the variables will be
called

* `$foo_path`
* `$foo_settings_path`
* `$foo_variable_path`

* Note that these variables will point to the latest installed version of
  `Foo`, instead of the version listed in the Dependency file.*<!-- it seems
  better to me to emphasize this fact -->

* Also note that special characters will be replaced with underscore. If, for
  example, GTK+ is listed in the Dependency file, the variable will be called
  $gtk__path, and Tcl-Tk will be $tcl_tk_path.*


# Patches 

Patches are applied in filename order, with the `-p1` option.  Creation by

```
 diff -Naur old_dir new_dir
```

or

```
 diff -Nau old_file new_file
```

works well. They should be named `01-explanation.patch`, where the initial
numbers increase in the order for patches to be applied, and `explanation` is
a short title giving some inkling of the patch's purpose. Additionally, the
first few lines of the patch (before the

```
 --- foo/1.0/file.bad
 +++ foo/1.0/file.good
```

lines) should contain an explanation of why the patch is necessary. GoboLinux
avoids patches to add features or optimizations; patches should fix
compilation or installation, or true bugs.


## Dynamic patches 

These patches are modified by Compile prior to being applied. They should be
named `01-explanation.patch.in`. [Dynamic variables](#dynamic-variables) may
be used, prefixed with the string `@%Compile_` and postfixed with `%@`. Such
variables include (where the Program being compiled has some dependency
`Foo`):

* `@%Compile_target%@`
* `@%Compile_settings_target%@`
* `@%Compile_variable_target%@`
* `@%Compile_foo_path%@`
* `@%Compile_foo_settings_path%@`
* `@%Compile_foo_variable_path%@`


# Resources/ 

The Recipe subdirectory `Resources/` can contain various metadata.  These
files are copied to `/Programs/Foo/Version/Resources` upon installation. All
these files are optional except for Dependencies and Description.


#### BuildDependencies 

This file lists dependencies which must be present to successfully compile the
Program.  They may include compilers or build tools.  The format is the same
as Dependencies, below.

#### BuildInformation 

Informational file about which versions of dependencies were actually linked
against when compiling.

#### `Defaults/`

This is a directory which may contain, in `Defaults/Settings`, the default
contents of the `/Programs/Foo/Settings` directory.  The contents of this
directory will be reconciled with the currently active settings, if any, by
[[UpdateSettings]].  The original defaults will remain in
`/Programs/Foo/Version/Resources/Defaults`, so that a user may revert to them as
necessary.

`Defaults/` may also contain a subdirectory `Variable/`.  These files are copied
to `/System/Variable/`, if not already present.

#### Dependencies 

This file lists programs which should be installed for this Program to work properly.
The format is like

```
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

The tags such as `[lame]` specify [[Use Flags]], optional dependencies which
affect the compilation of the package, if present.

When the range string (i.e., `=`, `>=`, etc) is omitted, the dependency
resolution algorithm assumes it to be `>=`.

The exact algorithm for complex dependencies is specified in
[[CheckDependencies]] but allows for a sequence of options separated by `|`
(or) each of which is a sequence of versions separated by "," (and). 
Precedence is left to right.  Thus:

```
    GCC < 4.0.0 | >= 4.1.0, != 4.1.2 | ICC > 2.0.0 
```

means a GCC version less than 4.0.0 or a GCC version greater than 4.1.0 but
not equal to 4.1.2 or an ICC version greater than 2.0.0.  See the code for
[[CheckDependencies]] for the exact algorithm.

Dependencies to language-specific package managers can be fulfilled using the
[[Aliens]] subsystem, using the syntax `AlienType:alien_package`, as in
the examples above.

Note that there are limitations in version handling for Aliens, as it depends
on the Alien provider and the package manager itself:

* CPAN dependencies ignore version information ([CPAN only installs the latest
  version](http://stackoverflow.com/questions/260593/how-can-i-install-a-specific-version-of-a-set-of-perl-modules))

For more info, see [[Dependencies]] and [[Use Flags]].


#### Description 

This file contains information of interest to humans regarding the program.  A
typical example is

```
[Name] GCC 
[Summary] The GNU Compiler Collection 
[Description] The GNU Compiler Collection contains frontends for C,  C++, 
Objective-C, Fortran, Java, and Ada... 
[License] GNU General Public License (GPL) 
[Homepage] http://gcc.gnu.org/ 
```

#### Environment 

This file contains environment variables which should be set for this program,
as bash assignments. For example, the Firefox recipe has

```
export MOZ_PLUGIN_PATH=${goboLibraries}/browser-plugins
```

#### Hints 

These contain hints for UpdateSettings on when to overwrite, delete, or skip
updating of certain settings. See [[Hints File]].

#### PostInstall 

A bash script which is executed by [[Compile]] (or [[InstallPackage]]) after
installation.  This is for one-time actions which should not be associated
with any stage of the compilation or installation process, but run after the
Program is symlinked.  They are kept separate from the Recipe file so that
they are retained in binary packages which may be distributed.

#### Requirements

These list conditions that must be met on the system, but which do not entail
an action unless they're not met. The only implemented requirements so far are
`required_users` and `required_groups`.

Entries in `required_groups` can have a gid parameter, as seen in this example:

```
required_groups=(
  "users"
  "yes gid=90125"
)
```

Individual entries in `required_users`, on the other hand, can have
uid=<num> and groups=<name[,name]*> options, as in:

```
required_users=(
  "scripts"
  "wakeman uid=2112 groups=yes,users"
)
```

See the [mailing list
thread](http://thread.gmane.org/gmane.linux.distributions.gobo.devel/2267).

#### Tasks/

Files in this subdirectory are [[boot script tasks]], linked to `System/Tasks`.
These are roughly equivalent to the `/etc/init.d` scripts found in many
distributions.

#### Wrappers/

This subdirectory contains scripts which are typically GoboLinux-specific
wrappers for commands in the installed package. They may call the real program
with options or environment appropriate for a GoboLinux system. They are
linked into the `/System/Index/bin` directory along with the normal binaries.

