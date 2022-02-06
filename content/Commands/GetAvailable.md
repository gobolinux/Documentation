---
title: "GetAvailable"
---

```
GetAvailable
 Get available packages, recipes and tracked versions.


Options:
 -t [t1,t2,...]
 --types=[t1,t2,...]  sets what kind of packages can be searched, in the
                      passed order. Valid types are:
                       local_package, official_package, contrib_package,
                       installed, recipe, tracked, all
                      using only the first character from any of the above
                      is also valid:
                       l, o, c, i, r, t, a
                      Default types are:
                       local_package, official_package
                      notice that when "recipe" type is used, Compile.conf is
                      read to set recipe-store locations and local recipes
                      locations.

 --local-dirs=[d1,..] where to look for local binary packages. By default,
                      uses the paths defined at GetAvailable.conf

 --force-update       downloads required packages list even if there is a
                      local copy (cached in /Data/Variable/tmp/Scripts-jroth/cache/) newer than one hour.

 -W, --no-web         do not try to download anything and don't lists
                      remote recipes and packages (if not explicitly listed
                      in '--types='). Overrides '--force-update'

 -p
 --gobo-programs      Override default /Programs as path of installed packages
```

Examples of usage:
```fish
GetAvailable --types=recipe
```