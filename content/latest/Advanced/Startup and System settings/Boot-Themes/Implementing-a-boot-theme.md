---
title: "Implementing a boot theme"
weight: 2
---

This section describes how each of the obligatory theme functions must be
implemented.

## ThemeInit

This, as the name implies, is the standard location to perform initializations.
Below is an example on how you can use the standard `$PREVLEVEL` variable (from
the Sysvinit `init` program) to echo some message when system initializes or
goes down.

```shell
if [ "$PREVLEVEL" = "N" ]
  then
    echo "GoboLinux is initializing..."
  else
    echo "GoboLinux is going down..."
fi
```

## ThemeFile

GoboLinux boot scripts work by processing a sequence of files (again, check
section
"[Customizing the initialization](Customizing_the_initialization "wikilink")"
for more details). Before starting to process each of these files, the boot
scripts core will call `ThemeFile` passing as the first (and only) parameter the
name of the file that is starting to be processed. Needless to say, you are not
obligated to give feedback on what file is being processed (the "Hat" theme,
example, does nothing in its implementation of `ThemeFile`.

A very simple example implementation of `ThemeFile` follows.

```shell
function ThemeFile() {
  echo "Entering file '$1'..."
}
```

## ThemeBefore and ThemeAfter

These functions wrap the execution of commands. `ThemeBefore` runs before a
program is executed and `ThemeAfter`, as expected, afterwards.

`ThemeBefore` is given two parameters: an identifier and a message. The
identifier is a numeric id so you can match calls to `ThemeBefore` and
`ThemeAfter`. Likewise, `ThemeAfter` is given two parameters, the identifier and
a numeric result code, indicating success (zero) or failure (other values).

If your theme supports only sequential booting (ie, does not use `Fork` and
`Wait` to parallelize the execution of the boot tasks), you can ignore the
identifier -- most themes do, as sequential boots are more common and that makes
the themes simpler. On parallel boot, however, programs can end in a different
order than they were started; with some escape code trickery, one can represent
graphically the intrincacies of parallel booting (the CheckList theme is an
attempt at that).

Here's a quick example of `ThemeBefore` and `ThemeAfter`:

```shell
function ThemeBefore() {
  shift # ignore id
  echo -n "===> $@... "
}
function ThemeAfter() {
  if [ "$2" -eq 0 ]
    then echo "{SUCCESS}"
    else echo "{ERROR}"
  fi
}
```

## ThemeFinish

The `ThemeFinish` function is called as the last step in a runlevel switch
(after everything else was done). Hence, this is the place to add any
finalization code. A common task performed by `ThemeFinish` is writing to the
issue file, whose contents are displayed on the screen just before the login
prompt. The issue file name is passed as the first (and only) `ThemeFinish`
parameter.

The following example shows a sample `ThemeFinish` implementation that just
writes an issue file that clears the screen.

```shell
function ThemeFinish() {
    clear > $1
    echo "Welcome!!" >> $1
}
```
