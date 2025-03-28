---
title: "The Recipe file"
weight: 3
---

The Recipe file contains a series of directives using shell assignment and shell
function syntax. Supported directives presented below, divided into categories:

-   [Getting the source](getting-the-source) - tells Compile how to fetch the
    software
-   [Recipe types](recipe-types) - tells Compile which tactic to use to compile
    the software
-   [Other directives](other-directives) - further customize the compilation
    process.
-   [Hooks](Hooks)
-   [Dynamic Variables](Dynamic-variables)
-   [Patches](Patches)
-   [`Resources/`](Resources1)


A minimal recipe will have at least two directives, one specifying how to get
the source (such as `url`) and `recipe_type` to tell what is the method to use
when building it.
