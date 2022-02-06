---
title: "GoboLinux Filesystem Hierarchy"
weight: 4
---

Here is an overview of the GoboLinux filesystem tree. The legacy folders
(on the ":" part of the tree) are links to the corresponding GoboLinux
folders. The legacy folders are excluded from default directory view by
[GoboHide](/Documentation/GoboHide).

```
/ 
|-- Data                  - for resources belonging to the system and to individual programs 
|   |-- Compile           - sources, recipes and other files used by the Compile tool
|   |   |-- Archives 
|   |   |-- LocalRecipes
|   |   |-- PackedRecipes
|   |   |-- Recipes
|   |   `-- Sources 
|   `-- Variable          - for spool files, log files, temporary files, etc.
|       |-- cache 
|       |-- empty 
|       |-- lib 
|       |-- lock 
|       |-- log 
|       |-- run 
|       |-- spool 
|       `-- tmp
|-- Mount                 - mountpoints for filesystems
|-- Programs              - where programs (with all their files) are installed 
|-- System
|   |-- Aliens            - files managed by programming language package managers
|   |-- Environment       - links to program files declaring environment variables
|   |-- Index             - links to files in each program's
|   |   |-- bin               + bin/ and sbin/ directories
|   |   |-- include           + include/ directory
|   |   |-- lib               + lib/ directory
|   |   |-- libexec           + libexec/ directory
|   |   `-- share             + share/ directory
|   |       |-- consolefonts
|   |       |-- fonts 
|   |       `-- man
|   |            |-- info     + info/ directory
|   |            `-- man{1-9} + man{1-9}/ directories
|   |-- Kernel
|   |   |-- Boot          - kernel images, config files and programs needed to boot
|   |   |-- Devices       - device files (managed by Udev).
|   |   |-- Modules       - loadable kernel modules (device drivers)
|   |   |-- Objects       - a view of the kernel's device tree 
|   |   `-- Status        - kernel status files (belonging to the /proc filesystem)
|   |-- Settings          - system config files and links to files in program's Settings/ directories.
|   |   `-- BootScripts   - scripts used for boot, symlink to /Programs/BootScripts/Settings/BootScripts/
|   `-- Tasks             - links to programs' boot tasks (from their Resources/Tasks/ directory)
|-- Users                 - contains users' home directories
:
:
:-- etc   -> System/Settings 
:-- dev   -> System/Kernel/Devices
:-- sys   -> System/Kernel/Objects
:-- proc  -> System/Kernel/Status
:-- var   -> System/Variable
:-- tmp   -> System/Variable/tmp
:-- sbin  -> System/Index/bin
:-- bin   -> System/Index/bin
:-- lib   -> System/Index/lib
:-- lib64 -> System/Index/lib
`-- usr
    |-- X11R6   -> .
    |-- local   -> .
    |-- bin     -> ../System/Index/bin
    |-- sbin    -> ../System/Index/bin
    |-- include -> ../System/Index/include
    |-- lib     -> ../System/Index/lib
    |-- lib64   -> ../System/Index/lib
    |-- libexec -> ../System/Index/libexec
    `-- share   -> ../System/Index/share
```
