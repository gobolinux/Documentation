---
title: "Alien Packaging Subsystem"
weight: 3
---

## Alien Packages

GoboLinux has a concept of "Alien" packages. These are programs that are usually packaged via external, distro-independant package managers.
Common examples are: pip (Python), npm (Javascript), cargo (Rust), LuaRocks (Lua), RubyGems (Ruby), CPAN (Perl.

GoboLinux currently supports the following backends:
 - LuaRocks
 - PIP3
 - RubyGems
 - CPAN

## How to install and update Alien packages

In order to install a foreign package we can use the following syntax:

```fish
sudo Alien --install <package_manager>:<package_name>
```

For example in order to install or update meson you would type:

```fish
sudo Alien --install pip3:meson
```

## Limitations

Sadly, at the moment we are lacking support for some popular package managers like npm or cargo.

If you want to contribute support for these package manager look here: https://github.com/gobolinux/AlienVFS/tree/master/gobo/alienvfs
