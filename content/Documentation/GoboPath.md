---
title: "GoboPath"
---

This script is used everywhere inside many scripts. It exports shell variables
such as `$goboExecutables`, `$goboUsers`, `$goboKernel`, and so on, which
contains a string specifying where in the file system these entries are
(`/System/Index/bin`, `/Users`, `/System/Kernel`, and so on).

For example, in the `Scripts` package, within the `bin/` subdirectory are files
such as `ScriptFunctions` or `SuggestUpdates`, among others. These source
`GoboPath` via:

```fish
. GoboPath
```

This is normally within the `Scripts` package, at `bin/GoboPath`. The whole
GoboLinux hierarchy is kept as referential prefix in that file. The variable
`$goboPrefix` keeps track as to where GoboLinux is mounted at.

Let's avoid hardcoding things, sourcing this file and using these variables
makes the world a better place :-)
