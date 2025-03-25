---
title: "Files that cannot be symlinks"
---

Symbolic links play a major role in a GoboLinux system, but some programs don't
behave as expected when they are used. This section lists the files that cannot
be symlinks.

_"That is the reason why /System/Settings is not /System/Index/Settings: it does
not only contain links, by definition (or, better put, by necessity)" -- Hisham
Muhammad_

-   `/System/Settings/sudoers`

The configuration file for _sudo_ must be a regular file. If it is not, `sudo`
will complain and do nothing.

-   `/System/Settings/passwd` and friends

The settings files used by the Shadow package are quite interesting.
Theoretically, they can be symlinks, but there is a caveat: utilities like
useradd don't just modify these files; they remove and recreate them as regular
files. Hence, in practice, they cannot be symbolic links.
