---
title: "Suggestion for a less super user reliant update process"
---

The current update process in gobolinux requires super-user privileges.  This is sub-optimal.

In the following, a rough sketch of how to remedy this is proposed.

## Add a `gobo` user/group by default

* The primary user of the system will be added to the the `gobo` group during installation.
* Add a sudoers snippet that allows members of the `gobo` group to run system-update related scripts with no password for convenience
* Ensure that `/Data/Compile/{Archives,Recipes,Sources}` are reset to `chown -Rc gobo:gobo` and `chmod ug+rw` on each system-update related script run, possibly in a function (a script version of which should be part of the set of commands allowed to run without a sudo password for convenience).
* Find a clever way to not clutter commands that require being run as `root` or `gobo` -- possibly using functions?
  * This should make it easy to discern which commands need what privileges.

