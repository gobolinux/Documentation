---
title: "DeduceName"
---

Scan a file to find the capitalization of a program name.

## Usage
```fish
DeduceName <file> <name>
```

The script scans the given file looking for instances of name, and
returns which is the most frequent capitalization used.

## Example
```fish
DeduceName README gtkglarea
```
