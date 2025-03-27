---
title: "How to commit recipes"
weight: 6
hidden: true
---

{{% notice warning %}} This article is potentially out of date!! Please refer to
the "[GitHub Contributor Workflow]({{%relref GitHub-contributor-workflow %}})"
article instead! {{% /notice %}}

This page is for GoboLinux contributors who have been granted commit access to
the recipes repository. The privilege is intended to help those who frequently
contribute recipes. If you'd like to have commit access (or would like to
nominate a fellow user to get commit access) contact the developers (gobo at
gobolinux.org) and we'll work things out.

To commit recipes, you need the `DevelScripts` package installed, and
`Subversion`. The good news is that you don't need to manipulate Subversion
directly; the `DevelScripts` take care of that.

## Installing DevelScripts

You should fetch `DevelScripts` from CVS. This can be done using its Compile
recipe. Just run:

```fish
Compile develscripts
```

This will add a file called
`/System/Settings/DevelScripts/CompileSubversion.conf` -- take a look at this
file. It lists the default locations where `DevelScripts` expects to find the
local copy of the Subversion repository. You could change these locations, but
for simplicity let's keep the provided default: `/Data/Compile/Subversion`

## Committing recipes

To commit a recipe, use the `PutRecipe` script. It takes care of incrementing
the revision number, copying the files into the local repository and runs svn to
commit them to the GoboLinux repository. `PutRecipe` takes as a parameter a
directory containing a recipe, like this:

```fish
PutRecipe firefox
```

By default, it will look for a recipe in `/Data/Compile/LocalRecipes`. If there
is more than one version there, the script will complain and will ask you to
give it a second parameter specifying the version number.

Note that committing the recipe to SVN does not immediately generate a tarball
of it in the public recipe store. Recipe store updates are done periodically
from the svn repository in an automated fashion.

A useful link, in case you missed it in the
[Community](http://gobolinux.org/?page=community) page of the website is the
[web interface for the SVN repository](http://gobolinux.org/websvn/).

## Reviewing other people's recipes

If you have commit access to the recipes repository, feel free to provide
feedback on and commit recipes contributed by users to the
[gobolinux-recipes](http://lists.gobolinux.org/mailman/listinfo/gobolinux-recipes/)
mailing list. Be sure to provide feedback, even if just a quick email saying
"Committed, thanks!", so that other committers know that the recipe has been
already committed.

You don't need to actually compile the recipe in order to test it, but only
commit recipes that "look good" (have no problems reported by `RecipeLint`,
etc.) If the recipe does advanced stuff such as including patches to C code or
jumps through hoops in the hook functions, you may want to leave it so that more
experienced committers review it. Committing more straightforward recipes (such
as `NewVersion` updates) already helps a lot in "balancing the work load" for
committers, allowing devs to work on the more problematic cases.

## In case of doubt

If you're unsure about anything about a recipe, don't hesitate to use the
[gobolinux-recipes](http://lists.gobolinux.org/mailman/listinfo/gobolinux-recipes/)
mailing list to ask questions, submit recipes for discussion, etc.
