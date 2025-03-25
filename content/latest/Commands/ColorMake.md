---
title: "ColorMake"
---

In default GoboLinux systems, `make` is an alias to `ColorMake`.

## Multiple CPUs

Users on dual-core and similar high-end machines may want to take advantage of
existing CPU capabilities. This can either be done via the MAKEOPTS option or by
modifying the simple ColorMake script.

At

```fish
makecmd=
```

Edit the line to i.e.:

```fish
makecmd='/bin/make -j5'
```

About the `-j5` part, the rule of thumb is that the number after `-j` should
equal the number of your cores +1: on a typical dual-core machine, the number
would be 3.
