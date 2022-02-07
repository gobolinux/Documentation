---
title: "ProblemReport"
---

```fish
Scripts version: 016.01
Compile version: 016.01-r1
BootScripts version: 016.01-r1
Glibc version: 2.24
Linux-Headers version: 4.7.4
Xorg-Lib version: 7.7-r1
GCC version: 6.2.0-r4
Python version: 3.6.0-r5
KDE-Libs version:
Linux version: 4.9.4-r1
--help version:

Installed versions of --help

Compile.conf

# Add your name here so that credit is added to recipes.
#compileRecipeAuthor=""

compileDir="${goboPrefix}/Data/Compile"
compileDependenciesDir="$compileDir/Recipes"
compileArchivesDir="$compileDir/Archives"
compileSourcesDir="$compileDir/Sources"

compileRecipeDirs=(
   "$compileDir/LocalRecipes"
   "$compileDir/Recipes"
)

# List Store mirrors here
getRecipeStores=(
   "http://gobolinux.org/recipe-store"
)

# Where GetRecipe places its recipes.  Should be in $compileRecipeDirs
compileGetRecipeDir="$compileDir/Recipes"

# These specify the source and destination to GenRecipeStore
compileLocalRecipesDir="$compileDir/LocalRecipes"
compilePackedRecipesDir="$compileDir/PackedRecipes"

# Main free software repositories
ftpGnu=ftp://ftp.gnu.org/gnu
#ftpGnu=ftp://ftp.unicamp.br/pub/gnu
ftpAlphaGnu=ftp://alpha.gnu.org/gnu
httpSourceforge=http://downloads.sourceforge.net
#httpSourceforge=http://voxel.dl.sourceforge.net/sourceforge

UseFlags.conf
# List your use flags, one per line, prefixed with a + to enable
# or a - to disable. Lines starting with # are ignored as comments.
# If a space-separated list of programs is given after the flag specification,
# the specification only applies to those programs.
# Note that if multiple use flags with same functionality is enabled, e.g.
# "ssl", "openssl", "gnutls" and "nss", the default implementation is choosen
# by the recipe author
# Example declaration:
#+foo
#+bar
#-bar foo quux
#-baz

# Generic flags specify a functionality to be enabled, and may list
# several different specific flags that provide it.
# Specific flags are ordered by preference for each generic flag. Only the
# first valid specific flag will be enabled for each generic flag.
ssl: openssl gnutls nss
gui: qt4 qt3 gtk2 fltk gtk1 lesstif
qt: qt4 qt3
gtk: gtk2 gtk1
sql: sqlite mysql postgresql
tui: ncurses
sound: alsa jack pulseaudio arts nas
spellcheck: enchant aspell ispell hspell gnome-spell
file_monitor: fam gamin
rtl: pango graphite
sametime: meanwhile
zeroconf: avahi mdnsresponder howl monozeroconf bonjour rendezvous
ac3: a52dec
diracvideo: schroedinger dirac
xmp: exempi
ldap: openldap
desktop_search: strigi beagle tracker
gadu_gadu: ekg
motif: openmotif lesstif

GenericFlags.conf
```
