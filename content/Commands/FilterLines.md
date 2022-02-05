---
title: "FilterLines"
---

A flexible grep-like tool.

Examples:

    cat foo.txt | Filterlines "bla"

shows all lines from foo.txt that contain the regexp "bla"

    cat foo.txt | Filterlines "bla" "goob"

shows all lines from foo.txt that contain the regexp "bla" OR the regexp
"goob"

    cat foo.txt | Filterlines "bla" "goob" -n "mac"

shows all lines from foo.txt that contain the regexp "bla" OR the regexp
"goob" but NOT the regexp "mac"

    cat foo.txt | Filterlines "bla" "goob" -n "mac" "ops"

shows all lines from foo.txt that contain the regexp "bla" OR the regexp
"goob" but NEITHER "mac" OR "ops"

    cat foo.txt | Filterlines "bla" -n "goob" "mac" "ops"

shows all lines from foo.txt that contain the regexp "bla" and don't
contain "goob", "mac" or "ops"

    cat foo.txt | Filterlines -n "bla" "goob" "mac" "ops"

shows all lines from foo.txt that don't contain "bla", "goob", "mac" or
"ops"
