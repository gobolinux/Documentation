This page is intended to document the workflow from setting up Compile.conf for proper attribution, to Compiling and testing a package, to creating a commit with a good commit message to finally submitting a GitHub Pull Request (PR).

## Compile.conf and attribution

Fire up your favourite editor, open `/Programs/Compile/Settings/Compile/Compile.conf` and edit the `compileRecipeAuthor` key as appropriate:

```
# set up proper attribution for GitHub pull requests
compileRecipeAuthor="A. Random Contributor <somebody@some-email-address>"
```

If you are not comfortable using your real name, using a nick/alias is also acceptable.

For more options, check out the dedicated [Compile.conf] page.

## Create a GitHub pull request using `ContributeRecipe`

In short, ContributeRecipe does the following:

* Creates a fork of the Recipe tree on the user's GitHub space
* Creates and checks out a branch on said fork
* Commits the modifications to the given package in said branch
* Sends a PR to the GoboLinux project

### Set up git to use the correct user GitHub account

FIXME: This needs a proper re-think.