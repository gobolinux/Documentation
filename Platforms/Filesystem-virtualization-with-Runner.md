Runner is a brand new filesystem virtualization tool, specifically designed for GoboLinux. It dynamically changes a process' view of /System/Index based on the program's Dependencies file.

Instead of using full-fledged containers (which carry an entire distro inside them!) just to avoid library conflicts when running an executable, in GoboLinux you can launch a program with Runner to make sure the filesystem view of the process will match its dependencies. Runner builds a custom mount table for the process, like container tools do, but without all the file duplication: it dynamically picks the correct parts of your /Programs tree. This approach is only feasible because in GoboLinux programs are logically organized in the filesystem.

# Preparing the filesystem view

All you have to do is to make sure the dependencies of the program you want to run are correctly listed under the program's [Resources directory](https://github.com/gobolinux/Documentation/wiki/Resources-files) -- more specifically, in the [Dependencies](https://github.com/gobolinux/Documentation/wiki/Resources-files#Dependencies) file at /Programs/Name/Version/Resources/Dependencies. You may list program names (e.g., "LibPNG"), specify a particular version (as in "LibPNG 1.4.4") or even let Runner pick the best version given a certain range (e.g., "LibPNG >= 1.4.0, < 1.5.0").

Most likely, the program you want to run will already have a sane Dependencies file -- every binary package we distribute will have one, just like every compilation recipe do.

# GoboLinux Runner and the Compile tool

Our Compile tool is fully integrated with Runner. When you type `Compile Foo`, Compile fetches the recipe for Foo and passes both the Dependencies and BuildDependencies files of that recipe to Runner. By doing so, we ensure that the right versions of the libraries, headers, and executables needed by that package will be mapped onto /System/Index.

# Spawning an application with Runner

For regular GoboLinux packages, simply type `Runner application_name`. Runner will figure from which entry under /Programs `application_name` comes from, and will create a custom filesystem view for that application by overlaying its dependencies over /System/Index.

For non-regular GoboLinux packages, such as third-party executables downloaded on your home directory, you can hand-craft a Dependencies file and then provide that file to Runner, as in `Runner -d MyDependenciesFile ./third_party_app`.

# Multi-arch setups

Running a 32-bit application on a 64-bit distro is no different with Runner. Provided that you have the 32-bit dependencies installed under /Programs (such as "Glibc/2.18-i686" and "Bash/3.1-i686"), the Dependencies file of your program simply needs to state the versions of the 32-bit packages it relies on. Afterwards, simply type `Runner application_name` and you are all set.
