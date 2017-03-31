```
NAME
       Dependencies -

SYNOPSIS
       Dependencies { [-c] { <package> [<version>] | -d <dep_file> } |

DESCRIPTION
       Queries dependencies in a GoboLinux package.

       -f <file> }

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

       -f, --file

              show dependencies of one file only.

       -c, --check

              check the package's dependency file, instead of generating one.

       -r, --reverse

              reverse dependency match: indicate who uses a given program.

       -a, --all

              inspect all files, not only those in 'bin', 'sbin' and 'lib'.

       -m, --missing-only

              Display missing dependencies only. (check mode only)

       -H, --higher-or-missing-only

              Display missing dependencies or higher versions only. (check mode only)

       -l, --list

              List dependency file, if any (generate if not present).

       -d, --dependencies-file

              Check for the dependencies listed in the given file.

       -e, --execute <entry>

              Execute the command on each missing/higher. (check mode only)

       -b, --batch

              Batch mode: avoid asking questions.

       -p, --programs <entry>

              <dir> to check dependencies against.

       -w, --write

              Write dependencies to Resources/Dependencies.

       -k, --keep-going

              Don't quit immediately if any executed program fails. (check+execute mode only)

   Notes:
              If no version is specified, Current is assumed.

       Released under the GNU GPL.

GoboLinux                                                March 2017                                          DEPENDENCIES(1)

```
