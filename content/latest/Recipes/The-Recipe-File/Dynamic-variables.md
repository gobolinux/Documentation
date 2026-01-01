---
title: "Dynamic variables"
weight: 6
---

## Dynamic variables

Compile automatically creates variables that can be used in the functions.

### System variables

To help you in recipe writing, Compile gives you the following run-time
variables to use, each referring to a specific filesystem hierarchy's member.

```
$VARIABLE       :       DEFAULT PATH
==============================================
$goboExecutables:       /System/Index/bin
$goboHeaders    :       /System/Index/include
$goboModules    :       /System/Kernel/Modules
$goboLibraries  :       /System/Index/lib
$goboPrograms   :       /Programs
$goboSettings   :       /System/Settings
$goboTemp       :       /System/Variable/tmp
$goboVariable   :       /System/Variable
```

Thus, if you're writing a recipe for some program which accepts configure
options and for which you need to manually specify a library path, you can use
the $goboLibraries variable like

```fish
configure_options=(
  "--with-extra-libraries=$goboLibraries/<path_to_the_library>"
)
```

The same applies to the remaining as well, depending on specific program's
needs.

### Program variables

For every recipe there will always be variables for the program prefix as well
as variables for the settings directory and the variable directory for the
program.

-   `$target`
-   `$settings_target`
-   `$variable_target`

For the recipe for `Foobar 2.1` those variables will have the values of
`$goboPrograms/FooBar/2.1`, `$goboPrograms/FooBar/Settings` and
`$goboPrograms/FooBar/<b></b>Variable` respectively.

### Dependency variables

There will also be variables for every dependency listed in the Dependency file.
If for example `Foo 1.2` is listed as dependency, the variables will be called

-   `$foo_path`
-   `$foo_settings_path`
-   `$foo_variable_path`

> [!NOTE]
> -   Note that these variables will point to the latest installed version of
>    `Foo`, instead of the version listed in the Dependency file.
>
> -   Also note that special characters will be replaced with underscore. If, for
>     example, GTK+ is listed in the Dependency file, the variable will be called
>    `$gtk__path`, and Tcl-Tk will be `$tcl_tk_path`.