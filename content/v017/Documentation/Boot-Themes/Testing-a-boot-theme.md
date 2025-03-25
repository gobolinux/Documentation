---
title: "Testing a boot theme"
weight: 3
---

Fortunately you don't have to reboot your computer to test every feature you add
to your boot theme. The `TestBootTheme` script is your friend. Just run it
passing your boot script name as a parameter:

```fish
TestBootTheme MyVeryOwnBootTheme
```

This will simulate a boot procedure with lots of things getting executed. Some
of them will be quiet, some will echo a lot of text, some will succeed, some
will fail... Just press enter when it ends up at the "login" prompt to finish.
If you don't give it a Theme name, it will output the list of available Themes
from `/Programs/BootScripts/Current/Themes/` instead.

Of course, this script is also useful to see how the various boot themes are, so
that you can choose which one is your favorite.

{{% notice note %}} Some themes may not display correctly in an
Xterm/Konsole/other graphical terminal, or with a non-standard console font.
It's probably best to run TestBootTheme in the same environment you boot in!
{{% /notice %}}
