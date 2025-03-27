---
title: "Writing Recipes"
weight: 3
---

There are two ways to create recipes:

1. Updating an existing one, or
2. Creating one from scratch.

The utilities for accomplishing this are:

[`NewVersion`]({{%relref "NewVersion" %}}), [`EditRecipe`]({{%relref "EditRecipe" %}})
and [`MakeRecipe`]({{%relref "MakeRecipe" %}}).

Once the recipe is done and compiled, a packed version of it will show up in
`/Data/Compile/PackedRecipes` (or the location specified in
`/System/Settings/Compile/Compile.conf`.

The GoboLinux developers encourage you to contribute your recipes, so that the
community can benefit.

To send a recipe for inclusion into the main `Compile` tree, just run
`ContributeRecipe <program name>` to submit it for review.

{{% toc %}}

## Setting up Compile.conf

We only need to do one thing here, add your name to `Compile.conf` (for credits
on recipes you may make). Open `Compile.conf` in a text editor such as `nano`:

```fish
nano /System/Settings/Compile/Compile.conf
```

On the 2nd line of text, there should be a line for the setting
`compileRecipeAuthor`. Uncomment it (remove the leading `#`), and enter your
name between the double quotes.

If you have any other recipe store URLs that you want to use (friends or your
other machines), add them to the `getRecipeStores` list.

Then save the file and exit `nano` (`Control`+`O`, `Enter`, `Control`+`X`).

## Updating old recipes

When a recipe for an older version of a given package already exists, you don't
need to run [`MakeRecipe`]({{%relref "MakeRecipe" %}}) again. Instead, use
[`NewVersion`]({{%relref "NewVersion" %}}) with the package name and version to
create a new recipe starting with the previous recipe contents. For example:

```fish
NewVersion GCC 4.4.4
```

This command will fetch the latest `GCC` recipe, create a new subdirectory
called `4.4.4` inside `/Data/Compile/Recipes/GCC` and will replace the package
version in `$url` by `4.4.4`.

You can also give the full URL for the package sources:

```fish
NewVersion GCC 4.4.4 ftp://ftp.gnu.org/gcc/gcc-4.4.4/gcc-4.4.4.tar.bz2
```

If the version of the package has not changed, and only minor recipe updates are
needed, [`NewVersion`]({{%relref "NewVersion" %}}) will not work as it will not
copy the same version of a recipe over. In this case,
[`EditRecipe`]({{%relref "EditRecipe" %}}) is the tool to use.

## Creating new recipes

If you are writing a recipe from scratch, the "[Recipe Format
Specification]({{%relref Recipe-Format-Specification %}})" documentation will prove
useful.

### Naming new recipes

One important, but often overlooked aspect of creating a recipe is naming it.
There are guidelines and tools to ease this process, but nothing beats common
sense really: keep in mind that the name you're giving to the recipe is the name
that will show up under `/Programs` and in the binary package name. Pick names
that won't look "out of place" in a GoboLinux setup.

You usually don't have to worry a lot about this: `Compile` and related tools
attempt to do their best to do this job for you, suggesting a name when one is
not explicitly given. But if you spot that it messed up, please abort
compilation and give it a good name as a parameter.

What's a good name? One that follows our set of package naming guidelines:

1. The app authors are sovereign about the capitalization, if they define it.
   Examples are: XFree86, LyX, Qt.
2. If the capitalization is undefined (ie, all-lowercase) or inconsistent (for
   example, showing up in different forms in the README), our set of
   capitalization rules, as defined by the
   [`NamingConventions`]({{%relref "NamingConventions" %}}) script, apply.
3. Applications are sovereign in defining their usage of hyphens and underscores
   to separate words in their names, when they are consistent.
4. Packages should never have spaces in their names. For example, use
   "AdobeReader" as the name, rather than "Adobe Reader" or "Adobe_Reader".
5. There should never be two package names differing only in capitalization. The
   GoboLinux scripts refer to package, program and recipe names in a
   case-insensitive manner.

The set of rules are defined in
[`NamingConventions`]({{%relref "NamingConventions" %}}) and deal with detecting
common prefix and suffix patterns, such as "Tools" and "Utils" and
vowel-consonant heuristics.

When a program name is not explicitly given to `Compile` (e.g., if it assumes it
from an URL), it passes the inferred name through
[`NamingConventions`]({{%relref "NamingConventions" %}}). In recent versions, some
rules are enforced even in explicitly given names -- one of them is that all
program names must start with a capital letter.

### MakeRecipe

In this example we'll make a recipe, starting from the source code for a program
on your computer. We'll use [joe](http://sf.net/projects/joe-editor/), a text
editor (console based). This is my first recipe, and it is now in the main
`Compile` tree.

```fish
MakeRecipe http://unc.dl.sourceforge.net/sourceforge/joe-editor/joe-3.1.tar.gz
```

Based on the filename of the URL, [`MakeRecipe`]({{%relref "MakeRecipe" %}})
detects that the program it is compiling is called joe (which, after a run of
the [`NamingConventions`]({{%relref "NamingConventions" %}}) script, becomes Joe),
and that the version is 3.1.

{{% notice note %}} In case it didn't, you could have passed it explicitly as
parameters: {{% /notice %}}

```fish
MakeRecipe HardToDetect 2.0 http://example.org/htd_2_0.tar.bz2
```

[`MakeRecipe`]({{%relref "MakeRecipe" %}}) should now report that it has downloaded
the sources, and found that it uses **autoconf**. Which is a good thing, as that
means there is very little work to be done on our part. So now we compile and
install the package on our machine.

```fish
Compile joe
```

Wait a few minutes, and Joe will be compiled and installed on your system.

When you create a new recipe for a program that's not yet available in the
GoboLinux recipe, please consider contributing it to the community! (See section
"[GitHub Contributor Workflow]({{%relref GitHub-contributor-workflow %}})" for
details.)

TODO: `Compile`'ing progams that don't use **autoconf**, ones that escape the
sandbox, etc.

### Meta Recipe

Writing Meta recipe is like putting small things inside some larger container.
For example consider the following meta recipe:

```fish
# Recipe for version 1.4.5 by Hisham Muhammad, on Wed Jan 23 01:28:21 BRST 2008
# Recipe (MakeRecipe) for Audacious by Andre Detsch <detsch@gobolinux.org>, on Wed Nov 30 15:01:27 BRST 2005
compile_version=1.8.2
recipe_type=meta
include=(
    "Audacious-Itself--1.4.5"
    "Audacious-Plugins--1.4.4"
)
```

Where two packages (`Audacious-Itself` and `*-Plugins`) are being regrouped
behind 1 "bigger" recipe called `Audacious`. So with meta recipe you can have
lots of small recipes regrouped in one big recipe. It simplify installation and
can help too in some case with stubborn project that don't get along immediately
with Gobo's directory layout. Thus creating a meta recipes can help porting
quickly a project in one big chunk (all the parts will be installed into the
same prefix), before making it nicer and modular later.

## Share your recipes

Share your recipes with the Gobo community! Recipes you create or update will be
located in `/Data/Compile/Recipes`. Consider using a text editor to write a
Description file for your recipe before you share it.

To share your recipe, use this command:

```fish
ContributeRecipe <program name>
```

[ContributeRecipe]({{%relref "ContributeRecipe" %}}) will submit a Pull Request on
GitHub so that the project maintainers can review it and merge it. Please note
that you will need a valid account at github.com in order to contribute recipes.

Approved committers should refer to these [
Guidelines]({{%relref "How-to-commit-recipes" %}}) (others should use
[`ContributeRecipe`]({{%relref "ContributeRecipe" %}}).)
