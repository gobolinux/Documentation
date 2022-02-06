---
title: "RebuildLinks"
---

Rebuild `/System/Index directories`.

```
Usage: RebuildLinks <option>

Options:

-   -h, --help - Shows this help.
-   -v, --version - Show program version.
-   -V, --verbose - Enable verbose mode.
-   -s, --shared - Rebuild /System/Index/share.
-   -n, --environment - Rebuild /System/Environment.
```

Not all directories in the /System/Index hierarchy can be rebuilt using
this tool because it would render the system in an inconsistent state
during the program's execution.

Examples:
```fish
RebuildLinks --shared
```
