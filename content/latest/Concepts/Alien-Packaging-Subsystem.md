---
title: "Alien Packaging Subsystem"
weight: 4
---

## Alien Packages

GoboLinux has a concept of "Alien" packages. These are programs that are usually packaged via external, distro-independant package managers.
Common examples are: pip (Python), npm (Javascript), cargo (Rust), LuaRocks (Lua), RubyGems (Ruby), CPAN (Perl).

GoboLinux currently supports the following backends:
 - LuaRocks
 - PIP3
 - RubyGems
 - CPAN

## How to install and update Alien packages

Main article: [**Managing Alien Packages**]({{%relref "Managing-Alien-Packages" %}})

## Limitations

Sadly, at the moment we are lacking support for some popular package managers, like npm or cargo.

If you want to contribute support for these package manager look here: https://github.com/gobolinux/AlienVFS/tree/master/gobo/alienvfs
