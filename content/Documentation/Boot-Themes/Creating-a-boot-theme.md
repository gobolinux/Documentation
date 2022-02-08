---
title: "Creating a boot theme"
weight: 1
---

This section explains how you can create your own boot script theme.

Section "The boot scripts anatomy" already explained that a theme is a single
script file. In fact, if you really want, you can create a theme that spreads
through multiple files (but this is not necessarily a good idea). The point here
is that one file is enough. This file implements a five functions: ThemeInit,
ThemeFinish, ThemeBefore ThemeAfter, and ThemeFile.

So, if you want to create a boot theme for GoboLinux, all you have to do is to
create a script file like
`/Programs/BootScripts/*<version>*/Themes/MyVeryOwnBootTheme` that implements
those functions (and optionally something in the script body) with all the bells
and whistles you want.

### Subtopics:

1.  [Implementing a boot theme]({{<ref "Implementing-a-boot-theme" >}})
2.  [Testing a boot theme]({{<ref "Testing-a-boot-theme" >}})
