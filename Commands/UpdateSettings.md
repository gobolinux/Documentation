```
NAME
       UpdateSettings -

SYNOPSIS
       UpdateSettings [<options>] [<mode>] <program> [<version>]

DESCRIPTION
       Interactively update settings from defaults in Resources/Defaults/Settings

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

       -d, --diffs

              When a file has been modified, show differences.

       -c, --check

              Only check whether current settings differ from the defaults.

       -r, --report

              Only report whether current settings and defaults differ.

       -l, --list

              List files that differ between current settings and defaults.

       -u, --update

              Update settings (default)

   Update Modes:
       -a, --auto

              Update automatically, without prompting the user at any point

       -i, --interactive

              Update interactively, prompting the user before each change

       -q, --quick

              Quickly update, prompting only when there are conflicts (default)

       (C)2005 by David Smith. Released under the GNU GPL.

              Maintained by Dan Charney and the GoboLinux team

GoboLinux                                                March 2017                                        UPDATESETTINGS(1)

```
