---
title: "UseFlags"
---


`UseFlags`

Usage:
```fish
UseFlags [<program> [<flag-to-test>]]
```

When program and flag both specified, the return code is true if the flag is
enabled, and false otherwise.

If only program is specified, or `UseFlags` is called alone, output the set
of flags enabled for that program or overall.

program may be the path to a recipe directory to include only flags actually
used by prog.
