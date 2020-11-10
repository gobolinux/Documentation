## Live environment

### Running Compile

Install UnionFS-Fuse to workaround limitations with the sandbox in the Live environment:
```
InstallPackage https://gobolinux.org/packages/017/Fuse--2.9.7--x86_64.tar.bz2
InstallPackage https://gobolinux.org/packages/017/UnionFS-Fuse--2.1--x86_64.tar.bz2
```

## Installed system 

### Git-related errors when invoking Compile for the first time

Loopback network interface needs to be brought up. As root, run:

```
ifconfig lo up
echo ifconfig lo up >> /System/Settings/BootScripts/BootUp
```

### InstallPackage searches for packages from GoboLinux 016 rather than 017

Update the search URL used by the Scripts package:

```
GrepReplace -B "016" "017" /System/Settings/Scripts/GetAvailable.conf
```

### Update of Compile and Scripts tools

Compile and Scripts are always evolving. Make sure to update your copies by
running the following commands after you boot into your installed system for
the first time:

```
cd /Programs/Scripts/Current
git pull && UpdateSettings --auto Scripts && make

cd /Programs/Compile/Current
git pull && UpdateSettings --auto Compile
```

### Wrong version of SQLite

The version under /Programs/SQLite/3310100 is actually 3.8.2. Please run the
following commands to update to its most recent version:

```
Compile SQLite
RemoveProgram SQLite 3310100
```

### Dependencies files with reference to Ncurses

Ncurses has been replaced by NcursesW, but some packages' metadata still hold
references to the former. The following command fixes that:

```
GrepReplace -B "^Ncurses " "NcursesW " /Programs/*/*/Resources/Dependencies
```

## Outstanding issues

Some problems have been reported by our users and are currently being fixed by our team. They are:

- `ContributePackage` is not working -- use [[ContributeRecipe|GoboLinux GitHub contributor workflow]] instead.
- Cut-and-paste does not work out of the box from a VM. Compiling `spice-vdagent` and loading its daemon should fix that.