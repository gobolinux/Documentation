```
NAME
       SymlinkProgram -

SYNOPSIS
       SymlinkProgram [<options>] <program_name> [<program_version>]

DESCRIPTION
       Link a program from the /Programs hierarchy in the /System tree.

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

       -s, --settings <entry>

              Link settings into /System/Settings.  Valid entries are: 'yes' 'no' 'safe' The default value is 'yes'.

       -l, --libraries <entry>

              Link libraries into /usr/lib.  Valid entries are: 'yes' 'no' 'safe' The default value is 'yes'.

       -e, --executables <entry>

              Link executables into /usr/bin.  Valid entries are: 'yes' 'no' 'safe' The default value is 'yes'.

       -h, --headers <entry>

              Link headers into /usr/include.  Valid entries are: 'yes' 'no' 'safe' The default value is 'yes'.

       -a, --shared <entry>

              Link shared files into /usr/share.  Valid entries are: 'yes' 'no' 'safe' The default value is 'yes'.

       -w, --wrappers <entry>

              Link wrappers into /usr/bin.  Valid entries are: 'yes' 'no' 'safe' The default value is 'yes'.

       -t, --tasks <entry>

              Link tasks into /usr/bin.  Valid entries are: 'yes' 'no' 'safe' The default value is 'yes'.

       -x, --libexec <entry>

              Link libexec into /usr.  Valid entries are: 'yes' 'no' 'safe' The default value is 'yes'.

       -u, --unmanaged <entry>

              Defines  what  to  do  with unmanaged files in package.  Valid entries are: 'ask' 'install' 'skip' The default
              value is 'ask'.

       -E, --no-environment

              Do not link entries from /System/Environment.

       -F, --no-follow

              Do not follow symbolic links.

       -R, --no-requirements

              Do not process Resources/Requirements.

       -A, --no-variable

              Do not move variable files into /Data/Variable.

       -M, --no-doc

              Do not link manuals and info files.

       -C, --cleanup

              Clean up after installation.

       -c, --conflict <entry>

              What to do on conflicting symlinks.  Valid entries are: 'keep' 'overwrite' The default value is 'keep'.

       -f, --force

              Force symlinks. Same as '--conflict overwrite'.

       -n, --no-make

              Dummy option. Preserved for backwards compatibility.

       -r, --relative

              Use relative paths to link files from /Programs.

       -t, --rootfs

              Copy program to rootfs if a symlink.

   Notes:
              If no program version is specified, Current is assumed.

EXAMPLES
              SymlinkProgram WeirdSuperLib 2.4

COPYRIGHT
       Copyright © Hisham Muhammad, 2001-2005 - Released under the GNU GPL.

GoboLinux                                                March 2017                                        SYMLINKPROGRAM(1)

```
