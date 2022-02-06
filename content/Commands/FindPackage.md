---
title: "FindPackage"
---

`FindPackage`
Searches, chooses an occurence and prints where some package (or recipe) can
be found, based only on the program name (case insesitive) or on the
program name and program version.

```
Options:
 -t [t1,t2,...]
 --types=[t1,t2,...]  Sets what kind of packages can be searched, in the
                      passed order. Valid types are:
                       local_package, official_package, contrib_package,
                       installed, recipe, tracked, all
                      Using only the first character from any of the above
                      is also valid:
                       l, o, c, i, r, t, a
                      Default types are:
                       local_package, official_package
                      Notice that when "recipe" type is used, Compile.conf is
                      read to set recipe-store locations and local recipes
                      locations.

 --local-dirs=[d1,..] Where to look for local binary packages. By default,
                      uses the paths defined at GetAvailable.conf.

 --force-update       Downloads required packages list even if there is a
                      local copy (cached in /Data/Variable/tmp/Scripts-jroth/cache/) newer than one hour.

 -l, --full-list      Prints all the occurences that match the passed
                      parameters, not only the "best".

 -n, --newest-on-server  Tries to sort the result set by how recently the
                      packages have been modified on the server.
                      Automatically enables '--full-list'.

 -s, --substring      Match packages whose names contains the passed substring.

 -W, --no-web         Do not try to download anything and don't lists
                      remote recipes and packages (if not explicitly listed
                      in '--types='). Overrides '--force-update' and
                      '--newest-on-server'.

 -p
 --gobo-programs      Override default /Programs as path of installed packages
 ```

Examples of usage:
```fish
FindPackage kde
FindPackage kde 3.2.3
FindPackage KDE 3.2.3
FindPackage --types=recipe kde 3.2.3
FindPackage --types=local_package,official_package kde 3.2.3
FindPackage -t l,o kde 3.2.3
FindPackage --full-list kde 3.2.3
FindPackage --force-update --full-list kde 3.2.3
FindPackage --types=recipe kde-base 3.2.3
FindPackage --types=recipe --substring kd 3.2.3
FindPackage --types=installed gcc
```
