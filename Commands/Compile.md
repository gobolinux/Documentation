```
NAME
       Compile - Build software from GoboLinux recipe

SYNOPSIS
       Compile <program> [<version>]

DESCRIPTION
       Automated program compilation tool.

OPTIONS
       --terse

              Enable terse messages.

       --debug

              Enable debug messages.

       -h, --help

              Show this help.

       --version

              Show program version.

       -v, --verbose

              Enable verbose mode.

       --logfile <entry>

              Log all output to specified file.

       -n, --app-name <entry>

              Override application name.

       -e, --version-number <entry>

              Override version number.

       -c, --configure-options <entry>

              Options to be passed explicitly to './configure'.

       -k, --keep

              Keep files if program directory already exists.

       -b, --batch

              Batch mode: avoid asking questions.

       -B, --no-build

              Do not build, just fetch the sources.

       -I, --no-install

              Do not actually install the program.

       -W, --no-web

              Do not check remote site for recipes, and bypass fetching of archives.

       -S, --no-symlink

              Do not symlink. Deprecated - use --symlink=no instead.

       -l, --symlink <entry>

              If  symlinks  should  be  created  and wether they should be forced on conflicts.  Valid
              entries are: 'yes' 'no' 'force' The default value is 'yes'.

       -T, --no-strip

              Do not strip executables.

       -G, --no-sign

              Do not sign program.

       -U, --no-updatesettings

              Do not update settings for the program

       -M, --no-unmanaged

              Do not install unmanaged files.

       -L, --lazy

              'Lazy mode': cut some corners when rebuilding; debugging aid: do NOT use it for building
              packages.

       -A, --start-at <entry>

              Skip sub-recipes when building a meta-recipe: start include list at given recipe; effec‐
              tive only with --lazy; debugging aid: do NOT use it for building packages.

       -D, --no-dependencies

              Do not try to fulfill dependencies.

       -i, --install-separately

              If the application is part of a meta recipe, do  not  install  it  into  the  containing
              application but install it into a separate directory.

       -a, --remove-archive

              Remove archive(s) after a successful build

       -s, --remove-sources

              Remove sources after a successful build

       -P, --no-postinstall

              Do not run the PostInstall script after installation

       -R, --no-requirements

              Do not process the Requirements script after installation

       (C)2003-2007 by Hisham Muhammad et al. Released under the GNU GPL.



GoboLinux                                     March 2017                                    COMPILE(1)
```
