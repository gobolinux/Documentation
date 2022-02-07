---
title: "Package Naming Guidelines"
weight: 5
---

1.  If the program name already has capitals (e.g. XFree86, LyX, Qt) use it
    exactly as is.
2.  If the name is all lowercase or inconsistent (for example, different forms
    in the README), our set of capitalization rules apply.
3.  If the application uses hyphens or underscores in the name, follow it
    exactly.
4.  GoboLinux packages should never have spaces in their names. "Acrobat Reader"
    should become "AcrobatReader", not "Acrobat_Reader".
5.  There should never be two package names differing only in capitalization.
    Package names differing only in capitalization should be considered to be
    two versions of the same app.

The [`NamingConventions`](/Commands/NamingConventions) script applies these
rules and several heuristics to generate a suitable GoboLinux package name from
an input.
