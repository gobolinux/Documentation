---
title: "DescribeProgram"
---

```
DescribeProgram
 Returns the description of the program, if available.

-Options:

 -a, --update-all     downloads all descriptions available at the servers and
                      cache them locally

 -m, --mode=<mode>    Output mode: html, terminal or ascii.

 -W, --no-web         do not try to download remote descriptions if they are not
                      locally available
```

Examples of usage:
```fish
DescribeProgram gimp
DescribeProgram -W gimp
DescribeProgram -a
```
