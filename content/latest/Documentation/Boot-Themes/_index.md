---
title: "Boot Themes"
---

GoboLinux is flexible enough to offer you a choice of themes to control how your
GoboLinux looks when starting up.

You can select a theme by setting `BootTheme=<ThemeName>` in
`/System/Settings/BootOptions`. Available themes include:

-   **`CheckList`** - Shows tasks and others that depend on them, then checks
    them off.
-   **`Hat`** - A Red-Hat look-alike: lots of colored `[ OK ]`s and `[FAILED]`s
    are echoed as things are initialized.
-   **`Progress`**, **`Progress-II`**, or **`Progress-III`** - Fancy themes that
    stress your terminal with tons of escape codes.
-   **`Quotes`** - Prints short random quotes to indicate success or failure of
    every initialized item.
-   **`Slack`** - This theme is inspired by the feel of old-school Slackware
    boots: no distracting messages, no colors, no special effects.

Check `/Programs/BootScripts/Current/Themes/` to see all the available themes.

You can use the TestBootTheme script to see how a boot theme looks like without
actually rebooting your computer. TestBootTheme is described on section [Testing
a boot theme]({{%relref "Testing-a-boot-theme" %}}).

You can also set the boot theme from GRUB by adding `BootTheme=<ThemeName>` to
the boot line. This can be handy if BootOptions file specifies a broken or
nonexistent theme, because GoboLinux will not boot without a valid one.

Physically, a GoboLinux boot theme is a single script file located in
`/Programs/BootScripts/*<version>*/Themes`.

The theme file is loaded by the boot scripts core, and is called once for every
runlevel change. Although interesting stuff can be done in the script body, a
compliant boot script has only to implement the following functions:

-   `ThemeInit`
-   `ThemeFile`
-   `ThemeBefore`
-   `ThemeAfter`
-   `ThemeFinish`

These functions are the hotspots that glue the theme and the boot scripts core
together.

-   [Creating a boot theme]({{%relref "Creating-a-boot-theme" %}})
-   [Implementing a boot theme]({{%relref "Implementing-a-boot-theme" %}})
-   [Testing a boot theme]({{%relref "Testing-a-boot-theme" %}})
