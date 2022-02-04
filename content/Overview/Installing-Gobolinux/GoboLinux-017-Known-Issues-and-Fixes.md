---
title: "GoboLinux 017 Known Issues and Fixes"
menuTitle: "Known Issues and Fixes"
weight: 1
---

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

### Update expired SSL certificates!

The recent [Let's Encrypt fiasko](https://www.reddit.com/r/PFSENSE/comments/pyce7q/sept_29th_lets_encrypt_intermediate_ca_expiration/) requires our users to update their certificate database on the system. Otherwise tools like `git`, `wget`, `Compile` etc might not work correctly.

The appropriate way to resolve this, is by running:

```bash
sudo Compile --no-check-certificate CA-Certificates
```
and

```bash
sudo sh /System/Index/bin/update-ca-certificates
```

afterwards.

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

### Outstanding issues

Some problems have been reported by our users and are currently being fixed by our team. They are:

- `ContributePackage` is not working -- use [[ContributeRecipe|GoboLinux GitHub contributor workflow]] instead.
- Cut-and-paste does not work out of the box from a VM. Compiling `spice-vdagent` and loading its daemon should fix that.
- Sometimes when trying to `Compile` an already-installed Program, the build process will fail (see [Compile bug 51](https://github.com/gobolinux/Compile/issues/51)).  Sometimes this can be worked around by first manually doing a `RemoveProgram <failing program>` before re-attempting to `Compile` it. Note that it is generally a _**Bad Idea™**_ to try to `RemoveProgram`, say, `Python3` like this as it will break `Compile`.

### Compile fails stating that some headers or libraries could not be found, when they are there

The installation process used by Compile had a problem in that certain extended attributes used by `overlayfs` were
carried over from the sandbox to the installation directory. Some of those extended attributes tell `overlayfs` to
consider the corresponding files or directories as deleted objects. Since we use `overlayfs` to sandbox the compilation
process, this bug may impact Compile in the sense that existing files may be considered as non-existent.

If you face this problem, please run the following commands on your installed system to remove those attributes:

```
fname=
xattr_pattern="trusted.overlay."
getfattr -P -R -d -m "$xattr_pattern" --absolute-names /Programs 2> /dev/null | while read i
do
   if echo "$i" | grep -q "^# file:"
   then
      fname="$(echo "$i" | awk {'print $3'})"
   elif echo "$i" | grep -q "^${xattr_pattern}"
   then
      xattr="$(echo "$i" | cut -d= -f1)"
      setfattr --remove "$xattr" "$fname"
   fi
done
```
