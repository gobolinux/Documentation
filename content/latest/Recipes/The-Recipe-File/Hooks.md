---
title: "Hooks"
weight: 4
---

## Hooks

Besides the declarative variables, recipes can also contain imperative commands,
in the form of bash shell functions. This is the order the functions are called
for each recipe type:

{{% notice note %}} `pre_patch` will not be called if there are no patches.
{{% /notice %}}

#### configure:

-   `pre_patch()`
-   patch, if any
-   `pre_build()`
-   configure
-   make
-   `pre_install()`
-   make install
-   `pre_link()`
-   symlink
-   `post_install()`

#### cabal:

-   `pre_patch()`
-   patch, if any
-   cabal configure (affected by `$runhaskell` and `$cabal_options`)
-   `pre_build()`
-   cabal build (affected by `$runhaskell`)
-   `pre_install()`
-   cabal install (affected by `$runhaskell`)
-   symlink
-   `post_install()`

#### makefile:

-   `pre_patch()`
-   patch, if any
-   `pre_build()`
-   make
-   `pre_install()`
-   make install
-   `pre_link()`
-   symlink
-   `post_install()`

#### manifest:

-   `pre_patch()`
-   patch, if any
-   `pre_install()`
-   copy files
-   `pre_link()`
-   symlink
-   `post_install()`

#### python:

-   `pre_patch()`
-   patch, if any
-   `pre_build()`
-   python setup.py build
-   `pre_install()`
-   python setup.py install
-   `pre_link()`
-   symlink
-   `post_install()`

#### scons:

-   `pre_patch()`
-   patch, if any
-   `pre_build()`
-   scons.py
-   `pre_install()`
-   scons.py install
-   `pre_link()`
-   symlink
-   `post_install()`

#### xmkmf:

-   `pre_patch()`
-   patch, if any
-   `pre_build()`
-   xmkmf
-   make
-   `pre_install()`
-   make install
-   `pre_link()`
-   symlink
-   `post_install()`

### Private shell functions

For shell functionality to be shared, for example between sub-recipes of
different architectures, it is possible to define additional shell functions in
the recipe. Their names must be prefixed with `private__`.

### Use flag hooks

Additional shell functions `using_<flag>()` will be run for each use flag `flag`
which is set. Do not do anything in such a function which depends on time of
execution. Instead, use `using_<flag>_<hook>()`. For instance,
`using_gtk_pre_build()` is run at the time specified above, in the event that
the `gtk` use flag is set.

See [Use flags]({{%relref "Use-flags" %}}).

### New Hooks

Since version 1.12.0, Compile supports a new set of hooks. These hooks can be
used to override any of the steps in the compilation process, and are available
to all recipe types. As with the "old" hooks discussed above, the new hooks
shouldn't be necessary for most recipe types, but they are useful for cases in
which the compilation process needs to perform nonstandard steps.

In order of invocation, these are the new hooks:

-   `do_fetch()`
-   `do_unpack()`
-   `do_patch()`
-   `do_configuration()`
-   `do_build()`
-   `do_install()`

If any of these hooks are defined in your recipe, Compile will call it instead
of performing the standard corresponding step for the recipe type you are using.
So, for instance, if your recipe needs to perform the installation step in some
nonstandard way, your recipe should include something like this:

```fish
do_install() {
  # ... your code for nonstandard installation goes here ...
}
```

Notice that this will _not_ perform the standard configuration steps. If you
need to perform some nonstandard steps _in addition to_ the standard steps, you
can call the default Compile functions from your own hook. The function that
performs the default installation step for recipes of type manifest, for
instance, is called `manifest_do_install()`. Using it would look like this:

```fish
do_install() {
  # Perform the regular installation (for recipes with manifest type)
  manifest_do_install "$@"

  # Perform some additional, nonstandard steps
  # ... some ...
  # ... nonstandard ...
  # ... installation ...
  # ... steps ...
  # ... here ...
}
```