---
title: "GoboLinux Command Reference"
menuTitle: "Commands"
weight: 5
chapter:  false
pre: "<b>005 </b>"
---

## Package management

### Finding

-   [UpdateRecipesd](UpdateRecipes) - Update local copy of
    recipe store
-   [GetAvailable](GetAvailable) - Search for GoboLinux
    recipes and precompiled packages
-   [FindPackage](FindPackage) - Search for packages and
    recipes, locally or remotely.
-   [SuggestUpdates](SuggestUpdates) - List packages with an
    update available.
-   [SuggestDuplicates](SuggestDuplicates) - Provide a list
    of programs that are not linked to Current
-   [PrioritiseUpdates](PrioritiseUpdates) - Order output of
    [SuggestUpdates](SuggestUpdates) by dependency
-   [Dependencies](Dependencies) - Queries dependencies in a
    GoboLinux package.

### Installing

-   [Compile](Compile) - Compile and install software from
    sources using GoboLinux recipe.
-   [InstallPackage](InstallPackage) - Install precompiled
    GoboLinux packages.
-   [FetchArchive](FetchArchive) - Download the sources for a
    recipe, but don't compile them.
-   [Freshen](Freshen) - Many options to check for
    availability and upgrade GoboLinux packages

### Administration

-   [SymlinkProgram](SymlinkProgram) - Link a program from
    the /Programs hierarchy in the /System tree.
-   [DisableProgram](DisableProgram) - Unlink a program from
    the /System/Index hierarchy.
-   [RemoveProgram](RemoveProgram) - Remove a program version
    from the system.
-   [DetachProgram](DetachProgram) - Move a program from
    /Programs to a different location.
-   [RebuildLinks](RebuildLinks) - Rebuild /System/Index
    directories.
-   [RemoveBroken](RemoveBroken) - Remove broken links.

### Creating recipes and packages

-   [GetRecipe](GetRecipe) - Fetch a recipe and insert it in
    the recipes tree.
-   [MakeRecipe](MakeRecipe) - Create a recipe template.
-   [EditRecipe](EditRecipe) - Edit a recipe.
-   [ContributeRecipe](ContributeRecipe) - Submit recipe
    changes via a GitHub PR.
-   [CreatePackage](CreatePackage) - Make a GoboLinux
    package.
-   [NewVersion](NewVersion) - Update a recipe to a new
    version.
-   [PrepareProgram](PrepareProgram) - Prepares applications
    for instalation, running the 'configure'
-   [Hashes](Hashes) - Manages FileHash and FileHash.sig
    files in a GoboLinux package.
-   [MergeTree](MergeTree) - Mirrors one directory structure
    into another.

### Helper tools

-   [DeduceName](DeduceName) - Scan a file to find the
    capitalization of a program name.
-   [FiboSandbox](FiboSandbox) - Run the program in a
    protected sandbox, as a restricted user.
-   [FixInfo](FixInfo) - Remakes the entries in the info
    'dir' file.
-   [NamingConventions](NamingConventions) - Heuristics to
    determine a capitalized, GoboLinux-like name.
-   [SandboxInstall](SandboxInstall) - Runs 'make install',
    using a sandbox environment.

## System maintenance

-   [AddUser](AddUser) - Register a new user in this system.
-   [SystemFind](SystemFind) - Special 'find' utility for
    searches in the /System hierarchy.
-   [SystemInfo](SystemInfo) - Display some basic system
    information. Useful for /etc/issue.

## Utilities

-   [FilterColors](FilterColors) - Filter to monochrome.
-   [FilterLines](FilterLines)
-   [FixAttributes](FixAttributes) - Fix attributes from
    files based on its contents.
-   [GrepReplace](GrepReplace) - Swaps occurrences of a regex
    for another word in a series of files.
-   [IsExecutable](IsExecutable) - Determines if a file is
    executable.
-   [RemoveEmpty](RemoveEmpty) - Remove all empty directories
    inside current (or a given) directory.

## Wrappers

-   [FindQuick](FindQuick) (alias: f) - Find files.
-   [GrepQuick](GrepQuick) (alias: g) - Shorthand for 'grep'.
-   l - alias for 'ls' with some options set.
-   [KillProcess](KillProcess) - Enhanced process killing
    utility.
-   [Rename](Rename) - Performs a sed-based search/replace in
    a set of filenames.

## Boot scripts

-   [BootDriver](BootDriver) - The boot controller script.
-   [StartTask](StartTask) - Run a boot task from the command
    line.
-   [StopTask](StopTask) - Stop a boot task from the command
    line.

## Special files

-   [GoboPath](GoboPath)
-   ScriptFunctions
