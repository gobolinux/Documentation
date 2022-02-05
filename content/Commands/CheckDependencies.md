---
title: "CheckDependencies"
---

```
CheckDependencies
 Check dependencies. No decent help yet.

Options:
 -t [t1,t2,...]
 --types=[t1,t2,...]  Sets what kind of packages repositories that can be
                      searched to match the dependencies.
                      Default list is set at Settings/Scripts/FindPackage.conf

 -s
 --add-self=          Tell if the program passed as parameter should be
                      returned too.

                      Can be set to:
                         never       - do not return the passed program
                         always      - return the passed program
                         if_required - return the passed program iff type or
                                       version from the program was not passed
                                       as paramater (default)

 -i
 --install-optional=  Install optional dependencies? 'always', 'never', 'ask'

 -b
 --batch              Same as --install-optional=always

 -m, --mode=          Can be set to:
                         missing  - report matches only for missing packages
                         updating - report all packages (dependencies from the
                                    passed program) that can be updated
                         all      - report matches for all dependencies, even
                                    it they are already installed
                         list     - only list the dependencies, without printing
                                    matches
                         convert  - convert a Dependencies file of a recipe to
                                    the coresponding Dependencies file for the
                                    compiled binary

 -W, --no-web         Do not access the internet.

 -R
 --no-recursive       Only the direct dependencies are considered

 -B
 --no-blacklist       Do not skip packages listed at Dependencies.blacklist

 --blacklist=         List of application names to blacklist

 --no-prompt          Do not prompt to install anything

 --quiet-progress     Do not show progress indicator

 -f
 --file               Check for the dependencies listed in the given file.

 -p
 --gobo-programs=     Override default /Programs as path of installed packages

 --local-dirs=[d1,..] Where to look for local binary packages. By default,
                      uses the paths defined at GetAvailable.conf.

Examples of usage:
 CheckDependencies kde-libs 3.5.0
 CheckDependencies kde-libs 3.5.0 recipe
 CheckDependencies -t official_package,recipe kde-libs 3.5.0 recipe
 CheckDependencies -t official_package,recipe kde-libs 3.5.0 recipe
```
