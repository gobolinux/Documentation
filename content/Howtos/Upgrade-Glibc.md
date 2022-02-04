---
title: "Update Glibc"
---

Hi, has anyone got any hints for glibc? I compiled 2.5.1 into
/Programs/Glibc/2.5.1 but which step should i do next?

(Ideally this should be expanded... i have static versions of tar, bzip,
bash, coreutils, binutils, make, but if i symlink brutally then ncurses
has some links, so I probably need to do something differently.)

------------------------------------------------------------------------

I was in an even worse situation, since I was using a dynamic version of
those programs. I totally trashed my system: every single program would
segfault, and then the kernel started to panic at boot time. But I've
found a solution which can be used either to fix the above ailment, or
to cleanly install a new Glibc.

1\) Boot using the live-CD.

2\) Mount your root partition to /Mount/Media.

&gt; mount /dev/hda6 /Mount/Media

3\) Install the version of Glibc you want. Note that the "-r" is
essential, otherwise your /Systems/Index/bin links will point to
subdirectories of /Mount/Media, which won't be mounted anymore after you
reboot.

&gt; goboPrefix="/Mount/Media" SymlinkProgram -r Glibc 2.5.1

4\) Relink against the new Glibc. If you forget this step, all non
statically-linked programs will segfault. If your boot process involves
any (which it probably does), you won't even be able to reboot!

&gt; chroot /Mount/Media ldconfig -v

-- [Gelisam](User:Gelisam "wikilink")

To make this relatively painless, make sure to compile Glibc with using
this command

&gt; Compile -l no Glibc

as it will stop Compile from symlinking Glibc after a successful compile
and install.
