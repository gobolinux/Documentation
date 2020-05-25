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