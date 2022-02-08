---
title: "Recipes"
weight: 3
chapter: false
pre: "<b>003 </b>"
---

Recipes are directions to [`Compile`]({{<ref "Compile" >}}) on how to configure,
build, and install a particular software package.

## Topics

-   [Online recipe browser](http://recipes.gobolinux.org/)
-   [Writing Recipes]({{<ref "Writing-Recipes" >}})
-   [Recipe Format Specification]({{<ref "Recipe-Format-Specification" >}})
-   [Recipes for precompiled software (such as Skype or Adobe Flash
    Player)]({{<ref "Binary-Recipes" >}})
-   [Sharing recipes]({{<ref "Writing-Recipes#share-your-recipes" >}})

## Commands

### Acquiring

-   [FindPackage]({{<ref "FindPackage" >}}) - Search for recipes and packages
-   [UpdateRecipes]({{<ref "UpdateRecipes" >}}) - Update local recipe cache from
    the recipe store.
-   [GetRecipe]({{<ref "GetRecipe" >}}) - Fetch a recipe and place it in the
    local recipe cache, /Data/Compile/Recipes/.

### Creating

-   [NewVersion]({{<ref "NewVersion" >}}) - Use an existing recipe as a template
    for a new software version
-   [MakeRecipe]({{<ref "MakeRecipe" >}}) - Create a recipe template from a URL.

### Modifying

-   [EditRecipe]({{<ref "EditRecipe" >}}) - Edit an existing recipe.
-   [RecipeLint]({{<ref "RecipeLint" >}}) - Make sure a recipe has no obvious
    errors.

### Submitting

-   [PackRecipe]({{<ref "PackRecipe" >}}) - Generate a packed recipe tarball
    from local recipe cache, ready for submission.
-   [ContributeRecipe]({{<ref "ContributeRecipe" >}}) - Submit a recipe to the
    recipe store for review and inclusion.
