---
title: "GetAvailable"
---

`GetAvailable.conf` is the file where you can configure paths and URLs used to
locate binary packages.

It is stored at `/Programs/Scripts/Settings/Scripts/GetAvailable.conf` -- which,
once installed, has a link at `/System/Settings/Scripts/GetAvailable.conf` (if
you're used to the GoboLinux tree, you should know by now that this is the same
as `/etc/Scripts/GetAvailable.conf)`.

These are the usual contents of the file:

The timeout (in seconds) when trying to fetch the packages list from a sever.

```shell
timeout=15
```

The paths from which local packages will be automatically be found. Notice that
both compressed (e.g. `/Depot/Packages/Qt--4.0.0--i686.tar.bz2`) and
uncompressed (e.g. `/Mount/SquashFS/Programs/Qt/4.0.0`) packages can be matched.

```shell
defaultLocalPackagesPaths=(
"/Depot/Packages"
"/Mount/SquashFS/Programs"
"/Mount/CD-ROM/Depot/Packages/"
"."
)
```

The URLS from which lists of official binary packages (packed by some core
developer) will be retrieved.

```shell
officialPackagesLists=(
'http://kundor.org/gobo/packages/official/MANIFEST.bz2'
'http://gobo.calica.com/packages/official/MANIFEST.bz2'
)
```

The URLS from which lists of contributed binary packages (contributed by some
user, and placed, without garanties, at our servers) will be retrieved.

```shell
contribPackagesLists=(
'http://kundor.org/gobo/packages/contrib/MANIFEST.bz2'
'http://gobo.calica.com/packages/contrib/MANIFEST.bz2'
)
```

The URLS from which lists of tracked versions will be retrieved. A tracked
version is a program version that actually may not have a correspondent Recipe
or binary package, but that is already made available by the program developers

```shell
trackedVersionsLists=(
'http://gobolinux.org/version-tracker/TrackedVersions.bz2'
)
```
