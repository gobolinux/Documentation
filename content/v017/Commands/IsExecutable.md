---
title: "IsExecutable"
---

Returns 0 (success) if the file looks like a Linux executable (starting with a
hash-bang magic or an ELF header), or 1 (failure) otherwise.

This helper is used by the [FixAttributes](../FixAttributes) script.
