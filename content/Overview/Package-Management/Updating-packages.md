---
title: "Updating packages"
weight: 3
---

## Overview

Use the [`UpdateRecipes`](/Commands/UpdateRecipes) command to refresh
your local cache of the GoboLinux recipe store.

You can query available updates using the utilities
[`SuggestUpdates`](/Commands/SuggestUpdates) and
[`SuggestDuplicates`](/Commands/SuggestDuplicates). The output of each of
these commands is suitable for piping into commands.

The [`FindPackage`](/Commands/FindPackage) and
[`GetAvailable`](/Commands/GetAvailable) commands may also be useful.

### Example Update Process

Keep in mind that most operations that change the file-system state in
Gobo require super user privileges:

#### Ensure that Scripts are up to date

```fish
cd /Programs/Scripts/Current
sudo git pull && sudo UpdateSettings --auto Scripts && sudo make
```

#### Ensure that Compile is up to date

```fish
cd /Programs/Compile/Current
sudo git pull && sudo UpdateSettings --auto Compile
```
#### UpdateRecipes - Update local copy of recipe store

```fish
cd /Data/Compile/Recipes
sudo UpdateRecipes
```

#### SuggestUpdates - List packages with an update available

```fish
cd /Data/Compile/Recipes
SuggestUpdates
```

#### Install updates

Currently, there is no way to update packages automatically. This used
to be done with the [`Freshen`](/Commands/Freshen) script, which is
currently not in working order.

Updates thus need to be installed manually via
[`InstallPackage`](/Commands/InstallPackage) or
[`Compile`](/Commands/Compile) as appropriate.
