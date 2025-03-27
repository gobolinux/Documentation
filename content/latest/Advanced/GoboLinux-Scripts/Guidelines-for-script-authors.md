---
title: "Guidlines for script authors"
linkTitle: "Guidelines for Developers"
weight: 3
---

This section documents the coding style used in GoboLinux shell scripts.

It's important to note that not all scripts follow these guidelines, because of
historical baggage (some of the scripts are older than GoboLinux itself).
Patches to correct the non-conformities are welcome.

## Indentation and block organization

A few rules of thumb:

-   Three spaces for indentation. Avoid joining `do` and `then` in the same line
    with `;`, instead put it on a line by itself, aligned with `for`, `while` or
    `if`.
-   Prefer using `if` rather than idioms like ` && { }`, but apply your common
    sense.
-   Be generous in you use of quotes whenever referring or defining variables,
    and the `${x}` syntax when merging variables inside strings.
-   Bear in mind that `esac` is ridiculous.
-   When doing weird stuff such as functional-like programming with eval, hide
    it in a pretty function to pretend it is a bit more readable. Eventually we
    might make a `Functional` module. By now, `Map()` is defined in the `Array`
    module.

It's hard to believe, but the only shell module containing GoboLinux-specific
stuff is the one aptly called `GoboLinux`. Keep that in mind when submitting
functions for inclusion in one of the modules.

## Names

The idea in the naming convention is to orthogonally describe scope and purpose
of each name. We define "local scope" as names that are specific to a given
script, and "library scope" as names defined in `Scripts` modules such as
[`GoboPath`]({{%relref "GoboPath" %}}), `ScriptFunctions` or one of the imported
function modules.

These are the guidelines:

-   Function names have underscores between words

Example: `local_function`, `Library_Function`

-   Variable names do not, they're just connected

Example: `localvariable`, `LibraryVariable`

-   Library names (for functions and variables) have capital letters

Example: `Library_Function`, `LibraryVariable`

-   Local names (for functions and variables) are in all-lowercase

Example: `local_function`, `localvariable`

-   All-uppercase variables are reserved for standard Unix usage

Example: `PATH`, `LD_LIBRARY_PATH`

-   Configuration variables used in [.conf
    files]({{%relref "Configuration-files" %}}) start with the script name in
    lowercase, resulting in a case style similar to that used in Java variables

Example: `compileRecipeDirs`, `editKeymapLayout`
