---
title: "ContributeRecipe"
---

```
NAME
       ContributeRecipe -

SYNOPSIS
       ContributeRecipe { <recipe dir> | <recipe name> [<recipe version>] }

DESCRIPTION
       Contribute a recipe to the global store

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

    -g, --gobo
        GoboLinux developer: push straight to repo.

    -p, --pretend
        Don't really submit, just dump the report to stdout.

    -s, --show-secret
        Show secret GitHub oauth token on stdout.

EXAMPLES
              ContributeRecipe firefox

COPYRIGHT
       Copyright © 2008-2009 Michael Homer, 2020 Rune Morling. Released under the GNU GPL.

GoboLinux                                                March 2017                                      CONTRIBUTERECIPE(1)
```

Usage examples:

```
ContributeRecipe <name>
```

```
ContributeRecipe Bash
```