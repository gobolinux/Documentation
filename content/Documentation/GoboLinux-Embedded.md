---
title: "GoboLinux Embedded"
---

## GoboLinux for ARM CPUs

The GoboLinux port for ARM CPUs has been happening with a focus on the armv5te,
having the XScale as optimization target. The entire process of development has
been done with the Bootstrap tool, described some sections below, which consists
on a menu based interface to select and compile packages. All of this is free
software and you're heavily encouraged to try it, enhance it and join us with
the development of GoboLinux for the embedded.

The next sections are going to show you how to download and install the ARM
port, pre-compiled packages and how to compile new packages from scratch, using
the Bootstrap tool.

## Downloading GoboLinux-ARM

In order to make things easier for embedded developers, GoboLinux is currently
shipping two versions of the ARM port: one consisting of a small (yet
functional) initrd, and another containing the full version, with graphical
desktop and tools suited for the end-user.

It's very common to install the initrd image in the flash and then mount the
bigger image from a NFS server or from another media, such as an SD card. This
is how we're currently proceeding, and it has been doing quite good. One can
then perform a `chroot`/`pivot_root` in the full media, or just union-mount both
images by putting the command in the initrd's boot script.

The tarballs for the initrd and for the full version can be fetched here:

-   [initrd](http://gobo.calica.com/gobolinux-iso-arm/GoboLinux-003-armv5te-ramdisk.gz) -
    4.3MB compressed, 12.5MB uncompressed
    [(md5)](http://gobo.calica.com/gobolinux-iso-arm/GoboLinux-003-armv5te-ramdisk.gz.md5)
-   [Full version](http://gobo.calica.com/gobolinux-iso-arm/GoboLinux-003-armv5te.tar.gz) -
    63MB compressed, 162MB uncompressed
    [(md5)](http://gobo.calica.com/gobolinux-iso-arm/GoboLinux-003-armv5te.tar.gz.md5)

Alternatively, one can download the ISO image instead, which offers an
uncompressed file system created around Rocket-Ridge/Joliet extensions. The
following links provide access to the ISO and its checksum, respectively:

-   [Full version (ISO)](http://gobo.calica.com/gobolinux-iso-arm/GoboLinux-003-armv5te.iso) -
    280MB
    [(md5)](http://gobo.calica.com/gobolinux-iso-arm/GoboLinux-003-armv5te.iso.md5)

In order to uncompress the tarball with the full version, one must to supply the
'p' flag to tar, so that permissions are kept. Uncompressing the full version,
thus, is done through the following commands:

```fish
mkdir GoboLinux-003-armv5te
cd GoboLinux-003-armv5te
tar zxpf /path/to/GoboLinux-003-armv5te.tar.gz
```

Given that ARM platforms usually need to have their own special kernel image,
there's no point on shipping one with the distribution. There is, however, an
optional patch used to hide the legacy tree, so that only the GoboLinux tree
appears in the filesystem (`/System`, `/Programs` and so on). This patch is
called GoboHide, and it can be downloaded for various kernel releases on its
[documentation page]({{%relref "GoboHide" %}}).

## Installing the distribution

The installation is pretty much dependent on the platform used, but it's a
common thing to have a bootloader capable of downloading files over the serial
port or over the network and storing them at specific locations in the flash.
Take a look in the documentation for your platform to check how to update your
initrd.

## Configuring GoboLinux embedded

The initrd image is actually an gzip'ed ext3 filesystem, which can be extracted
and mounted on your local filesystem. In a GoboLinux system, the following
commands are enough to mount it read-write on any distribution:

```fish
mkdir -p /System/ARM-SoftFP
gzip -d GoboLinux-003-armv5te.gz
mount -o loop GoboLinux-003-armv5te /System/ARM-SoftFP
```

At this point, the filesystem will be available at `/System/ARM-SoftFP`, where
you'll be able to read and write its contents. It's important to note the
directory name used as mount point: since the filesystem was all compiled
against that prefix, all symlinks inside the image will be available and will
not be broken, with a few exceptions in the root filesystem.

The major configurable part of the distribution is sitted in `/System/Settings`.
You'll probably want to take a look at `/System/Settings/NetworkOptions` and at
`/System/Settings/BootScripts`, which holds the bootscripts. The latter has a
file named BootUp, which is the script launched by init at boot time.

There are also tasks, which are simple scripts with `start`/`stop` commands.
They are stored at `/System/Tasks`, where you'll see files such as GoboHide,
LoadModules, Mouse and Swap. Take a look there if you have something to modify
on these standard tasks.

After finished with the modifications, just leave `/System/ARM-SoftFP` and
compress the image again with the following commands:

```fish
umount /System/ARM-SoftFP
gzip GoboLinux-003-armv5te
```

You're now ready to upload your modified filesystem to your platform, according
to the instructions provided by your vendor.

## Installing new packages

There's a [repository](http://gobo.calica.com/packages/armv5te-softfp/) for
precompiled packages where you can download the available ones. These are not
stripped, though. They include headers, static libraries, documentations and all
sort of thing that one would expect from a standard package. If you need to
reduce their size, please take a look at the
[shrink scripts](http://cvs.savannah.nongnu.org/viewcvs/tools/Bootstrap/packages/?root=goboscripts)
inside each program's directory at
[Bootstrap's CVS tree](http://cvs.savannah.nongnu.org/viewcvs/tools/Bootstrap/?root=goboscripts).
There are many scripts already written for the available packages, and we
welcome new contributions to help us to reduce packages even more.

After the desired packages are downloaded, store them somewhere in your
filesystem and then run `InstallPackage <package.tar.bz2>`. The `InstallPackage`
script shipped with the `TinyScripts` package on ARM is not smart as the one in
the Scripts package, used on the i686 port, though. It doesn't look for
dependencies yet, so you still need to take a manual look at the file
Resources/Dependencies inside the unpacked program at /Programs. A minimal
support for dependencies is going to be added on the next versions.

## Getting help

Please subscribe to the
[GoboLinux ARM mailing list](http://lists.gobolinux.org/mailman/listinfo/gobolinux-arm)
[(archives)](http://www.wotfun.com/pipermail/gobolinux-arm/) for getting help
from our community. You can also visit us on #gobolinux at irc.freenode.net.

# The BootStrap tool

The process of creating a distribution from scratch involves many steps which
are very error prone. Bootstrap is a tool which concentrates many scripts for
these purposes, abstracted in a simple yet powerful menu based interface. It
also deals with cross-compilation automatically, so it can be used to create a
distribution targetting another architecture or the same one serving your host
operating system. _(If you're interested on doing cross-compilation, please take
a look below on
[how to prepare the cross-compiler's terrain](http://gobo.kundor.org/wiki/GoboLinux_Embedded#Preparing_the_cross-compiler.27s_terrain))_.

In short, Bootstrap is able to either compile new packages, or to start a new
port from scratch, performing the following steps:

-   Create a Gobo directory structure for the new port, populating it with a few
    necessary system files. The target directory is defined by
    `$cross_prefix_dir` in the cross config file;

-   Installation of BootScripts / TinyScripts package;

-   Compilation of packages selected by the user, running optional hooks defined
    in some individual packages;

-   Reduction of the filesystem's size by running scripts capable of doing:

    -   Removal of documentation;
    -   Removal of static libs;
    -   Removal of symbols on libraries and executables;
    -   Removal of unnecessary data with the help of hand-written scripts
        available in some packages;

-   Automated creation of ramdisk images.

## Configuration

Given that the cross config file had been written, using it is just a matter of
running `./Bootstrap`. This command is responsible of fetching descriptions for
the available packages and then opening a menu based interface where the target
platform can be configured. The following snippet shows the available options:

```
Bootstrap Configuration

    Build options  --->
    Base  system  --->
    Development  --->
    Fonts and XML parsers  --->
    Audio  --->
    Networking  --->
    X servers  --->
    Video and graphics  --->
    GTK  suite  --->
    Misc  --->
    Desktop  --->
    Shrink Options  --->
```

### Build options

The first entry allows to select the target platform on which the compilations
will be targeted to. Currently, Bootstrap's build menu presents profiles for
SH-4 and ARM processors, allowing a subsequent selection of a specific
implementation of the chosen processor. This allows Bootstrap to keep
configuration files specific to each platform, such as bootscripts, package
selection and so on:

```
Build options

    Cross-Compiling (ARM target)  --->
    ARM implementation (SiriuStar board)  --->
    Target profile (Embedded platform)  --->
    Network interface (DHCP configuration)  --->
---
    (2.6.16.18) Kernel version for Linux-Libc-Headers package
    (GoboLinux) Hostname
    (gobo) Super-user name
```

This configuration shows that we're going to create a distribution for an ARM
processor. More especifically, we're targetting it to the
[SiriuStar](http://www.tecnequip.com.br/ele_produtos.html) board, so any special
scripts needed by that board are going to be integrated automatically into the
filesystem. A practical example of such profile script is one that needs to read
a specific driver's /proc entry to update the RTC.

Apart from creating a distribution for ARM or SH-4, it's also possible to create
a distribution which will run in the same processor as the one executing the
script. So, if you're running on a x86 and would like to create an embedded
version of GoboLinux for the same architecture, it's just a matter of disabling
the cross-compiling feature of Bootstrap:

```
Cross-Compiling

    (X) Native compiling
    ( ) ARM target
    ( ) SH-4 target
```

The development of Bootstrap also took care of those who'd like to create a
distribution to another platform, but which didn't need to care about space.
This situation doesn't need to count on replacements for the standard GoboLinux
tools, neither on the strip of individual files so that the filesystem can fit
in the flash or hard disk. The selection of this kind of profile is possible
through the **Target profile** menu, where one of _Desktop_ and _Embedded_
options can be chosen.

```
Target profile

    (X) Embedded platform
    ( ) Desktop platform
```

One final step configuring the target's platform is choosing its network
connectivity. Due to the common fact that many bootloaders focused on the
embedded allows to boot the kernel with bootp and to assign IPs even before the
operating system is up, it might not be feasible to reconfigure the network
after the system has booted. To avoid having GoboLinux' bootscripts to
reconfigure the network, it's possible to disable that in **Network Interface**:

```
Network interface

    (X) Disabled
    ( ) DHCP configuration
    ( ) Manual configuration
```

One last important option is related to the kernel version on which headers will
be available to the filesystem. The generation of the headers is currently done
by an external script developed by Linux From Scratch guys, which is capable of
removing portions not used by userspace applications. The last version known to
work was 2.6.12.

The remaining options are related to the configuration of the hostname and the
super-user's name. The super-user name can later be modified by editing passwd
and shadow on the generated filesystem, as there's a big attention in Gobo
community to remove hardcoded references to **root** in applications.

### Package selection

The selection of packages that will be compiled can be done through the
subsequent menus. The menu entries are disposable in a way so that the _base
packages_ are always shown first, and optional packages built or linked against
them are shown later in the screen.

Selecting them is pretty much straightforward, so only the base system is going
to be described here. Many small systems can be created by just using this first
menu, so you can start populating your filesystem in small steps, starting with
this one.

```
Base system

        Libc implementation (Glibc)  --->
    [ ] Module Init Tools
    [*] BusyBox
    [*] LibGCC
    [ ] ZLib
    [ ] GPM
    [ ] GoboHide
    [ ] Listener
    [ ] Udev
---
    [ ] Ncurses
    [ ] Bash
```

This setup allows to configure a small environment, where only the BusyBox suite
will be available. It already features a replacement for udev (called mdev), so
the system is going to be fully functional. The LibGCC package is generated by
some libraries taken from by the cross-compiler that will be needed at runtime
by some applications. One final note is made to the Libc implementation: if the
target filesystem really needs to be **that** small, uClibc can be used instead
of the default, Glibc.

### Shrink options

This is one of the more interesting features of Bootstrap. Due to the nature of
GoboLinux packages, all files related to a given package are stored inside a
unique entry at /Programs. This makes it very easy to cleanup the filesystem and
find big packages, and even more to automate this process with the help of
per-package scripts.

Making these scripts aware of which files are _necessary_ and which ones aren't
needed to get the package up and running is an easy task to be performed on
GoboLinux, and are reflected through the following options in the shrink menu:

```
Shrink Options

    [ ] Remove and shrink as much as possible
    [ ] Remove headers
    [ ] Remove static libraries
    [ ] Remove libtool related files
    [ ] Remove pkgconfig related files
    [ ] Remove documentation
    [ ] Remove backup of the default settings
    [ ] Remove internationalization files
    [ ] Remove aclocal macros
        Removal of symbols (All symbols from executables and libraries)  --->
        Native language support  --->
```

Please note that there will be no automatic cleanup of the filesystem. You must
invoke the **make shrink** command so that it performs a backup of the generated
filesystem, followed by the cleanup based on the selected options.

## Running Bootstrap

Finished with the _menuconfig_ configuration, Bootstrap is ready to start doing
its work. The _Bootstrap_ script automatically invokes **make**, which on its
turn will download, compile and install all packages selected, according to the
following snippet:

```
PrepareTarget: Creating the GoboLinux tree...
PrepareTarget: Populating the device directory...
PrepareTarget: Creating the LibGCC package...
(...)
```

At the end of this process, the filesystem generated will be available at the
directory specified at the cross config file (usually under /System), and will
be ready for usage on the target platform. Files can always be modified manually
after they are generated, as they're not overwritten by subsequent _make_ calls.
The filesystem can then be shared for remote mounting over NFS at boot time, or
copied to different medias, depending on your interests and resources available
on your platform.

## Hacking it

If you're porting Gobo to an architecture which is not listed by Bootstrap, you
can create a new entry for it by editing `functions/Platforms` and `Config.in`
inside Bootstrap's root dir.

## Availability

BootStrap can be downloaded as a package or directly from the Subversion
repository. The current stable release is 1.1, and it can be downloaded
[here](http://gobolinux.org/download/bootstrap). SVN snapshots can be obtained
in the following way:

```fish
svn checkout http://svn.gobolinux.org/tools/trunk/Bootstrap
```

# Porting GoboLinux to a new embedded platform

So, do you want to try Gobo on a different architecture? That's cool, and that's
why this documentation was created for: we want to encourage you to join in the
developers' and users' corner with interesting experiments.

This documentation is here to guide you on porting Gobo to a new embedded
architecture. The steps, examples and tools shown on this document have reached
a stable branch, being used in projects such as the Brazilian's Digital TV
research, where a Gobo port to the SuperH has been done, as well as the Gobo ARM
port which happened in parallel in another projects.

The remaining sections are going to focus on 2 ways of porting Gobo to a new
system: by cross-compiling and by using an existing distribution as a basis to
compile packages using the Gobo hierarchy. The latter has not been written yet;
see http://www.gobolinux.org/index.php?page=doc/articles/porting_guide for
inspiration.

## Preparing the cross-compiler's terrain

While we try to make porting as easy as possible, doing this kind of task always
needs some background on the subject. Cross compiling a whole set of packages
and preparing the root filesystem requires that you have an understanding of the
boot process, of the manual installation of a kernel image, shell scripts and
many more. Reading other chapters of the GoboLinux Documentation Project might
help you to acquire some of that knowledge.

### Requirements

Finished with the introduction, let's make a list of what you'll need. Firstly,
this tutorial assumes that you have **a host computer running GoboLinux**. The
Gobo team has developed numerous tools to help on the automation of the system,
such as compiling programs based on simple description files, detecting the
latest versions of a given application, enjauling the compile process so that
the host system doesn't interfere in the compilation environment, and so on.

For this reason, the tools developed to aid on the port are based on Gobo's own
infrastructure. After all, since you're porting Gobo to a new architecture we
would at least expect that you're also running it on your host computer, right?

Secondly, you'll need **a working cross-compiler**. Since we're going to create
a distribution _from scratch_ to a different architecture than the one running
on the host system, that's the way we will generate programs to it. There are
many cross-compilers ready for usage out there, and some scripts that might help
you to prepare your own. The following projects and cross-compilers have been
tested and are recommended:

-   [Crosstool](http://kegel.com/crosstool): Consists in a set of scripts and
    patches to generate a toolchain for many architectures, such as Alpha, ARM,
    i686, IA64, MIPS, PowerPC, PowerPC64, SH4, Sparc, Sparc64, s390 and x86_64.
    The current toolchains used by Gobo developers were generated by this tool;

-   [CodeSourcery](http://codesourcery.com): This is the major source for ARM
    toolchains, and is one of the leading companies developing the ARM EABI. If
    you want to get a tested and ready-to-use cross compiler for ARM, this is
    the place to get one;

-   [uClibc toolchain](http://uclibc.org): If you're looking for a very small
    distribution it's probably better to look at this alternative. The uClibc is
    a tiny libc implementation which targets devices with small storage
    capabilities. Please note, however, that this might come with small
    performance penalty on some applications.

Finally, you'll need to write **cross-compiler rules for the Compile tool**.
Compile has the ability to create binaries to different platforms, so there's a
need to write a configuration file for the one you're going to use, respecting
the naming convention **`Cross-<ARCH>.conf`**, where ARCH will represent the
target architecture. Cross configuration files are stored at
**`/System/Settings/Compile`**.

### Describing Cross.conf files

The Compile tool ships 2 sample files for the ARM and SH4 architectures. Let's
give a look into the variables exported by them, taking the ARM rule as
reference:

-   `cross_kernel_dir`: specifies the path on which the kernel sources for this
    platform are found. Since it's very usual to maintain the kernel for the
    working platform on a special directory during development stage, you can do
    that and just specify its location here;

-   `cross_kernel_version`: for the same kernel, specifies its release, based on
    the `VERSION`, `PATCHLEVEL`, `SUBLEVEL` and `EXTRAVERSION` variables
    exported in the Makefile;

-   `cross_kernel_arch`: when cross compiling the kernel, one must call
    `make menuconfig ARCH=*kernel_arch_name`. Specify your architecture's name
    under the kernel tree here;

-   `cross_prefix_dir`: where in the host's filesystem the new filesystem tree
    will be stored;

-   `cross_toolchain_dir`: where in the host's filesystem the toolchain is
    installed;

-   `cross_sys_incdir`: path to `stdio.h` inside the toolchain's dir;

-   `cross_gcc_incdir`: path to `stdarg.h` inside the toolchain's dir;

-   `cross_cpp_incdir`: C include dirs (is an array) in the toolchain's dir;

-   `cross_gcc_libdir`: path to `libgcc.*` files in the toolchain's dir;

-   `cross_libc_libdir`: path to `libc.*` files in the toolchain's dir;

-   `cross_uname_m`: output for `uname -m` on the target machine;

-   `cross_configure_host`: parameter to the configure script when building
    applications based on autoconf (`-host=target_machine_string`). This string
    describes the CPU on which the binary generated will run on;

-   `cross_configure_build`: parameter to the configure script when building
    applications based on autoconf (`-build=build_cpu_string`). This string
    describes the CPU which is doing the cross-compiling;

-   `cross_optimization_flags`: optimization flags to be used by the cross
    compiler. A useful place to look for available options is the GCC info page;

-   `cross_compiler`: prefix to the cross-compiler's executable files, such as
    _`arm-xscale-linux-gnu-gcc`_ and _`arm-xscale-linux-gnu-strip`_.
