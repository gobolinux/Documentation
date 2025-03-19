---
title: "Recipes"
weight: 3
chapter: false
pre: "<b>003&thinsp;</b>"
---

Recipes are directions to [`Compile`]({{%relref "Compile" %}}) on how to configure,
build, and install a particular software package.

## Topics

-   [Online recipe browser](http://recipes.gobolinux.org/)
-   [Writing Recipes]({{%relref "Writing-Recipes" %}})
-   [Recipe Format Specification]({{%relref "Recipe-Format-Specification" %}})
-   [Recipes for precompiled software (such as Skype or Adobe Flash
    Player)]({{%relref "Binary-Recipes" %}})
-   [Sharing recipes]({{%relref "Writing-Recipes#share-your-recipes" %}})

## Commands

### Acquiring

-   [FindPackage]({{%relref "FindPackage" %}}) - Search for recipes and packages
-   [UpdateRecipes]({{%relref "UpdateRecipes" %}}) - Update local recipe cache from
    the recipe store.
-   [GetRecipe]({{%relref "GetRecipe" %}}) - Fetch a recipe and place it in the
    local recipe cache, /Data/Compile/Recipes/.

### Creating

-   [NewVersion]({{%relref "NewVersion" %}}) - Use an existing recipe as a template
    for a new software version
-   [MakeRecipe]({{%relref "MakeRecipe" %}}) - Create a recipe template from a URL.

### Modifying

-   [EditRecipe]({{%relref "EditRecipe" %}}) - Edit an existing recipe.
-   [RecipeLint]({{%relref "RecipeLint" %}}) - Make sure a recipe has no obvious
    errors.

### Submitting

-   [PackRecipe]({{%relref "PackRecipe" %}}) - Generate a packed recipe tarball
    from local recipe cache, ready for submission.
-   [ContributeRecipe]({{%relref "ContributeRecipe" %}}) - Submit a recipe to the
    recipe store for review and inclusion.
