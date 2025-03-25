---
title: "Environment variables"
---

Some environment variables influence the behavior of some GoboLinux tools. You
may want to set them. Just remember that GoboLinux uses zsh (not bash) as its
default shell, so you should edit `.zshrc` (not `.bashrc`). Zsh is a
Bourne-style shell, though, so the syntax you're used to is still valid.

Of course, if you really prefer bash (though we really recommend giving zsh a
try!), you can change your default shell using the `chsh` command. See the
`chsh` man page for details.

The `$EDITOR` variable should be set to your favorite text editor. Whenever a
GoboLinux tool needs to run an editor, it will run the one indicated in this
variable (in fact, this is not a GoboLinux variable, several programs use it).
