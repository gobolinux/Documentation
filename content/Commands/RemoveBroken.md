---
title: "RemoveBroken"
---

Given a file name, this script verifies if it's a broken link or not.
Being a broken one, it gets deleted.

This script is very useful when used together with `find` to find stray,
broken links.

Example:

`   find /System/Index | RemoveBroken `

This is functionally equivalent to

`   find /System/Index -xtype l -delete`

The source code to RemoveBroken can be found here:

<https://github.com/gobolinux/Scripts/blob/master/bin/RemoveBroken>