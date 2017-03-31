```
NAME
       InstallPackage -

SYNOPSIS
       InstallPackage <package_file>|<package_dir>

DESCRIPTION
       Install GoboLinux packages.

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

       -b, --batch

              Do not ask for confirmation.

       --use-contrib

              Look in contrib store as well.

       -D, --no-dependencies

              Do not try to fullfit dependencies.

       -I, --no-install

              Do not install, only locate and fetch the package.  Automatically enables '--keep'

       -S, --no-symlink

              Do  not  create  symbolic  links  in /System, just fetch and unpack the package. Deprecated - use --symlink=no
              instead.

       -l, --symlink <entry>

              If symlinks should be created and wether they should be forced on conflicts.  Valid entries  are:  'yes'  'no'
              'force' The default value is 'yes'.

       -k, --keep

              Do not remove downloaded packages.

       -s, --same <entry>

              What  to  do  when unpackaging over the same version.  Valid entries are: 'keep' 'remove' 'cancel' The default
              value is 'cancel'.

       -o, --old <entry>

              What to do with a previously existing version of a package if found.  Valid entries are: 'keep' 'remove' 'ask'
              'cancel' The default value is 'keep'.

       -u, --unmanaged <entry>

              Defines  what  to do with unmanaged files from package.  Valid entries are: 'ask' 'install' 'skip' The default
              value is 'ask'.

       -C, --no-sign-check

              Do not check the signature.

       -U, --no-updatesettings

              Do not update settings for the package

       -W, --no-web

              Do not check remote site for packages, and bypass fetching of archives.

   Notes:
              Default behavior for --same is 'cancel', for --old is 'keep'.

EXAMPLES
              InstallPackage Gimp--2.0.5.tar.gz

       Released under the GNU GPL.

GoboLinux                                                March 2017                                        INSTALLPACKAGE(1)

```
