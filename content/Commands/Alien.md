---
title: "Alien"
---

```
Usage: Alien --<mode> AlienType:alienpkg [...]

Valid options for <mode> are:
    --get-version
    --getinstallversion
    --greater-than
    --met|--within-range|--interval
    --have-manager
    --get-manager-rule
    --install

Valid options for AlienType are:
    CPAN
    LuaRocks
    PIP
    RubyGems

Example:
    Alien --install CPAN:XML::Parser
    Alien --install PIP:burn

```
