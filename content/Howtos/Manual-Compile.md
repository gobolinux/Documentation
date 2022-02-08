---
title: "Manual Compile"
---

Building and installing manually from source. _This should only be done if one
is unable to [create a recipe]({{<ref "Writing-Recipes" >}}) or as an excercise.
With very few exceptions, the work of creating a recipe is rewarded by the ease
of using [Compile]({{<ref "Compile" >}})._

{{% notice note %}} If you use a local tarball, be sure to have the tarball
placed at /Data/Compile/Archives. Also make sure you know whether you have a
recipe locally or not, if you ie do not have access to the www on that machine.
{{% /notice %}}

I'm using dosbox from CVS as an example here.

**First**, go into the folder where you have the source (**change directory**).

```
phed@Arjuna ~/]cd dosbox
phed@Arjuna ~/dosbox]
```

Run `PrepareProgram` with the option -t or --tree to generate the directory tree
in `/Programs/DOSBox/CVS`.

```
phed@Arjuna ~/dosbox]PrepareProgram -t DOSBox CVS
phed@Arjuna ~/dosbox]
```

Then run `PrepareProgram` again without options to run configure

```
phed@Arjuna ~/dosbox]PrepareProgram DOSBox CVS
```

```
PrepareProgram: Preparing...
PrepareProgram: Autoconf configure script detected.
```

```
checking build system type... i686-pc-linux-gnu
...
config.status: creating config.h
config.status: executing depfiles commands
phed@Arjuna ~/dosbox]
```

Then we have to do whatever is required in order to build the application. In
the case of DosBox we have to issue `make` in order to compile the program.

```
phed@Arjuna ~/dosbox]make
make[1]: L/bin/make  all-recursive
make[1]: Entering directory `/Users/phed/dosbox'
...
make[1]: Leaving directory `/Users/phed/dosbox'
phed@Arjuna ~/dosbox]
```

Next run `SandboxInstall` to install the program into the Programs-tree

```
phed@Arjuna ~/dosbox]SandboxInstall dosbox CVS
SandboxInstall: unionfs is available.  Using UnionSandbox!
SandboxInstall: Installing DOSBox...
...
SandboxInstall: Postprocessing Sandbox
phed@Arjuna ~/dosbox]
```

And at last, run `SymlinkProgram` to link it into the LHS tree.

```
phed@Arjuna ~/dosbox]SymlinkProgram DOSBox CVS
SymlinkProgram: Symlinking DOSBox CVS.
...
SymlinkProgram: Done.
phed@Arjuna ~-->dosbox]
```

And then we're done. Enjoy!
