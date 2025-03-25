---
title: "Notes on Command-Line switches"
---

Many scripts accept command-line options. All options feature a short,
one-letter form, and a long form. Following the GNU conventions, short form
options are preceded by a single hyphen (as in `-a`, `-b`) and long form options
are preceded by two hyphens (as in `--foo`, `--bar`).

### Order of Command-Line Arguments

All command-line options have to be passed first, before other types of
arguments (file names, package names, etc). In other words,

```fish
FooScript -m Foo
```

works, but

```fish
FooScript Foo -m      # WRONG! Switches must come first.
```

does not.

### Switches taking arguments

Some command-line options accept arguments. These arguments must be passed as
the word following the argument, both in short and long forms. For example, say
that `-s` and `--long` are options that take a parameter. This is the correct
way to use them:

```fish
FooScript -s value --long another
```

These are not recognized:

```fish
FooScript -s=value --long another      # WRONG! Use distinct tokens.
```

### Do not conglomerate

Each option should be passed in a separate token, even when in short mode. If
-a, -b and -c are options for an imaginary `FooScript`, then

```fish
FooScript -a -b -c blah.txt
```

is correct, but

```fish
FooScript -abc blah.txt      # WRONG! Options must be separated.
```

is not.

### Help

All scripts have a `--help` option (or, in short form, `-h`). When a program
that needs arguments is run without arguments, the help text will be displayed.
(Note: Actually, not all scripts conform to this yet, but this is being worked
on).
