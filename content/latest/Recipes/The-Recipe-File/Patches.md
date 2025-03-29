---
title: "Patches"
weight: 7
---

Patches are applied in filename order, with the `-p1` option. Creation by

```fish
diff -Naur old_dir new_dir
```

or

```fish
diff -Nau old_file new_file
```

works well. They should be named `01-explanation.patch`, where the initial
numbers increase in the order for patches to be applied, and `explanation` is a
short title giving some inkling of the patch's purpose. Additionally, the first
few lines of the patch (before the

```diff
 --- foo/1.0/file.bad
 +++ foo/1.0/file.good
```

lines) should contain an explanation of why the patch is necessary. GoboLinux
avoids patches to add features or optimizations; patches should fix compilation
or installation, or true bugs.

## Dynamic patches

These patches are modified by Compile prior to being applied. They should be
named `01-explanation.patch.in`. [Dynamic variables](#dynamic-variables) may be
used, prefixed with the string `@%Compile_` and postfixed with `%@`. Such
variables include (where the Program being compiled has some dependency `Foo`):

-   `@%Compile_target%@`
-   `@%Compile_settings_target%@`
-   `@%Compile_variable_target%@`
-   `@%Compile_foo_path%@`
-   `@%Compile_foo_settings_path%@`
-   `@%Compile_foo_variable_path%@`