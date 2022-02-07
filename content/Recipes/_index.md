---
title: "Recipes"
weight: 3
chapter: false
pre: "<b>003 </b>"
---

Recipes are directions to [`Compile`](/Commands/Compile) on how to configure,
build, and install a particular software package.

## Topics

-   [Online recipe browser](http://recipes.gobolinux.org/)
-   [Writing Recipes](/Recipes/Writing-Recipes)
-   [Recipe Format Specification](/Recipes/Recipe-Format-Specification/)
-   [Recipes for precompiled software (such as Skype or Adobe Flash Player)](/Recipes/Binary-Recipes/)
-   [Sharing recipes](/Recipes/Writing-Recipes/#share-your-recipes)

## Commands

### Acquiring

-   [FindPackage](/Commands/FindPackage) - Search for recipes and packages
-   [UpdateRecipes](/Commands/UpdateRecipes) - Update local recipe cache from
    the recipe store.
-   [GetRecipe](/Commands/GetRecipe) - Fetch a recipe and place it in the local
    recipe cache, /Data/Compile/Recipes/.

### Creating

-   [NewVersion](/Commands/NewVersion) - Use an existing recipe as a template
    for a new software version
-   [MakeRecipe](/Commands/MakeRecipe) - Create a recipe template from a URL.

### Modifying

-   [EditRecipe](/Commands/EditRecipe) - Edit an existing recipe.
-   [RecipeLint](/Commands/RecipeLint) - Make sure a recipe has no obvious
    errors.

### Submitting

-   [PackRecipe](/Commands/PackRecipe) - Generate a packed recipe tarball from
    local recipe cache, ready for submission.
-   [ContributeRecipe](/Commands/ContributeRecipe) - Submit a recipe to the
    recipe store for review and inclusion.
