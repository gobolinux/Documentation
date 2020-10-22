This page is intended to document the new GitHub workflow for contributing to GoboLinux.

## Compile.conf and attribution

Fire up your favourite editor, open `/Programs/Compile/Settings/Compile/Compile.conf` and edit the `compileRecipeAuthor` key as appropriate:

```
# set up proper attribution for GitHub pull requests
compileRecipeAuthor="A. Random Contributor <somebody@some-email-address>"
```

If you are not comfortable using your real name, using a nick/alias is also acceptable.

For more options, check out the dedicated [Compile.conf](../Compile.conf) page.

## Create a GitHub pull request using `ContributeRecipe`

In short, ContributeRecipe does the following:

* Creates a fork of the Recipe tree on the user's GitHub space
* Creates and checks out a branch on said fork
* Commits the modifications to the given Recipe in said branch
* Sends a GitHub PR to the GoboLinux project

### Set up git to use the correct user name and e-mail

Git needs to be set up to use the same git `user.name` and `user.email` combination as the one used in `Compile.conf` in the `compileRecipeAuthor=` key.

```
cd
git config --global user.name="A. Random Contributor"
git config --global user.email="somebody@some-email-address"
# list the git configuration
git config --get user.name
git config --get user.email
```

### Run ContributeRecipe

Once the attribution is correctly set up, it's time to run the `ContributeRecipe` script.

The script has been designed such that all there is to the contribution process is to suply a name and a version to `ContributeRecipe` like so:

```
sudo ContributeRecipe ExampleRecipe 0.0.1
```

NB! Please ensure that you use a GitHub account where your name/alias and e-mail address has been added as a verified GitHub identity when using `ContributeRecipe`.

`ContributeRecipe` will prompt for your GitHub username and password a couple of times, do its magic and the end result will be a nice pull request which will hopefully get merged.