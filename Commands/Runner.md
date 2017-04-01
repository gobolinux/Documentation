```
Executes a command with a read-only view of /System/Index overlaid with
dependencies extracted from the program's Resources/Dependencies and/or
from the given dependencies file(s).

Syntax: Runner [options] <command> [arguments]

Available options are:
  -a, --arch=ARCH           Look for dependencies whose architecture is ARCH (default: taken from
                            Resources/Architecture, otherwise assumed to be x86_64)
  -d, --dependencies=FILE   Path to GoboLinux Dependencies file to use
  -h, --help                This help
  -q, --quiet               Don't warn on bogus dependencies file(s)
  -v, --verbose             Run in verbose mode (type twice to enable debug messages)
  -c, --check               Check if Runner can be used in this system
  -f, --fallback            Run the command without the sandbox in case this is not available
  -R, --no-removedeps       Do not remove conflicting versions of dependencies from /System/Index view


```
