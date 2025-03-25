---
title: "FilterLines"
---

A flexible grep-like tool.

Examples:

```fish
cat foo.txt | Filterlines "bla"
```

shows all lines from `foo.txt` that contain the regexp `bla`

```fish
cat foo.txt | Filterlines "bla" "goob"
```

shows all lines from `foo.txt` that contain the regexp `bla` OR the regexp
`goob`

```fish
cat foo.txt | Filterlines "bla" "goob" -n "mac"
```

shows all lines from `foo.txt` that contain the regexp `bla` OR the regexp
`goob` but NOT the regexp `mac`

```fish
cat foo.txt | Filterlines "bla" "goob" -n "mac" "ops"
```

shows all lines from `foo.txt` that contain the regexp `bla` OR the regexp
`goob` but NEITHER `mac` OR `ops`

```fish
cat foo.txt | Filterlines "bla" -n "goob" "mac" "ops"
```

shows all lines from `foo.txt` that contain the regexp `bla` and don't contain
`goob`, `mac` or `ops`

```fish
cat foo.txt | Filterlines -n "bla" "goob" "mac" "ops"
```

shows all lines from `foo.txt` that don't contain `bla`, `goob`, `mac` or `ops`
