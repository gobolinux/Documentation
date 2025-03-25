---
title: "AugmentCommandNotFoundDatabase"
---

This commands augments the existing database for
[CommandNotFound](../CommandNotFound) suggestions with data from the running
system. In other words, it looks at which executables exist in the installed
system and adds them to the `/Data/CommandNotFound.data` file from Scripts.

This is useful to improve the quality of the "command not found" suggestions.
Users are encouraged to send patches to Scripts improving the
`CommandNotFound.data` database.
