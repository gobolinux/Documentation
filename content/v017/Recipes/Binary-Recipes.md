---
title: "Binary Recipes"
weight: 3
---

Binary recipes (recipes that install precompiled binaries of software, rather
than compiling it from source) are permitted but discouraged where possible.
These recipes should have `_bin` suffixed to the version number as a marker, for
example `Sun-JDK 1.6.0_03_bin`, even where there is no corresponding source
recipe.

Source recipes are preferred where possible, as these allow optimisation and
bugfixing, but binaries are acceptable in some circumstances. In general, a
binary recipe will be accepted if it meets one of the following criteria:

1.  The software is only available in this form from the vendor. `Sun-JDK` is an
    example of this.
2.  Compiling the software cleanly is not possible or plausible on GoboLinux
    yet. Programs using the Maven build system are an example of this.
3.  The vendor provides prebuilt binaries in addition to the source, and:
    1.  The software is sufficiently large for compilation to be a large task
        with little gain (OpenOffice)
    2.  The vendor binaries are customised in some fashion, or multiple parallel
        products from the same source are built with different tasks (the
        various Eclipse builds: -Java, -C++, -EE, etc). In this case, the
        program name should be specific to the type of build: `Eclipse-Java`,
        `Eclipse-SDK`.
4.  The software requires a copy of itself to build, and isn't shipped with the
    default system. GHC is an example of this. In this case, the binary version
    should be named differently: `GHC-Bin` installs the pre-built GHC, which can
    be used to compile the source `GHC`.
5.  A source recipe would present some difficulty, and nobody has made one yet.

Each program is assessed individually, and some may be accepted outside these
guidelines. In any case, it never hurts to ask or submit a recipe if you're
unsure.

## Guidelines for binary recipes

-   Submitters should append an extra `_bin` string to the application's
    version. This is the adopted convention to identify binary recipes.
-   Everything specific to a given architecture shall be inside its arch subdir.
    This includes `url=`, `file=`, `file_md5=`, `file_size=` and any functions
    dealing with specific tarball contents that might change from one
    architecture's tarball to another. MD5 sums are especially important for
    binary recipes are they are used to assess the validity of the installed
    data, which could not be verified as usual by looking at the sources. Make
    sure the `file_md5` entry exists.
-   Distribution license must be filled in `Resouces/Description`. If the
    license is unknown, `Resources/Description` should set it as
    `[License\] Other` (or the license name as appropriate), and a file named
    `Resources/COPYING` should contain the license in question. "Known licenses"
    are those found in these
    [OSI list](http://www.opensource.org/licenses/alphabetical) or the
    [FSF list](http://www.fsf.org/licensing/licenses/).
