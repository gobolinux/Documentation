---
title: "Freshen"
---

Checks for updated GoboLinux recipes and packages

```
Usage:

    Freshen [ <opts> ] [ <list> ]

Options:

-    --binaries, -b - Include binary packages [default]
-    --cache-only, -c  - Update caches only
-    --debug  - Enable debug mode
-    --downgrades, -d  - Include downgrades
-    --empty-tree, -e  - Behave as though the installed program tree
    were empty - include dependencies all the way back
-    --excluding, -x  - Do not include *list* or anything with a
    dependency in it
-    --help, -h  - Display this help
-    --info, -i  - Get information on <program>
-    --limit, -l <n>  - Include no more than *n* updates
-    --lower-limit, -L <n>  - Skip the first *n* updates
-    --no-binaries, -B  - Do not include binary packages
-    --no-cache, -C  - Do not use cached data for /Programs
-    --no-downgrades, -D  - Do not include downgrades.  [default]
-    --no-recipes, -R  - Do not include recipes
-    --no-upgrades, -N  - Do not include upgrades
-    --recipes, -r  - Include recipes  [default]
-    --shallow, -s  - Shallow mode: don't include any upgrades that
    aren't strictly necessary. Requires *list*
-    --upgrade-system, -U  - Upgrade all programs, or *list* and
    dependencies if specified.
-    --upgrades, -n  - Include upgrades  [default]
-    --verbose, -V  - Enable verbose mode
-    --version, -v  - Show program version

Common options are:

-   -U for system updates
-   -l <n> to limit the number of updates to a few at a time
-   -s to limit the updates to those strictly necessary
-   -R to skip recipes and perform no compilation
-   -i <program> to get information on <program>
```

Freshen outputs its update lists in the form:

    [IUX] Foo 2.0                    1.0

Meaning an upgrade to Foo version 2.0, from 1.0, which is available as both a
recipe and a package.

The mnemonics mean:

-   **I** - Installed
-   **U** - Upgrade
-   **D** - Downgrade (color code: red)
-   **R** - Recipe available (color code: green)
-   **B** - Binary available (color code: yellow/brown)
-   **X** - Recipe and binary available (color code: blue)

Examples:

```fish
Freshen
```

Produce an ordered list of everything that can be updated on the system.

```fish
Freshen -R
```

Produce an ordered list of everything that can be updated on the system using
only binary packages.

```fish
Freshen -U -l 5
```

Update the first five programs on the list.

```fish
Freshen -U Firefox
```

Update Firefox and its dependencies

```fish
Freshen -U -x Qt
```

Update everything except Qt and anything that depends upon it.

```fish
Freshen -s Firefox Kopete
```

Ordered list of upgrades **needed** in order to upgrade Firefox and Kopete to
their newest releases. Add **-U** to perform the upgrade.
