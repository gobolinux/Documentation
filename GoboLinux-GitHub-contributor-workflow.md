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
git config --global user.name "A. Random Contributor"
git config --global user.email "somebody@some-email-address"
# list the git configuration
git config --get user.name
git config --get user.email
```

### Check for changed files in the Recipes repository

It is considered good practice to double check the changes about to be committed by ContributeRecipe:

```
cd /Data/Compile/Recipes
git status
# if existing files have been modified, you can run:
git diff
```

### Run `ContributeRecipe`

Once the attribution is correctly set up and the changes have been double checked, it's time to run the `ContributeRecipe` script.

The script has been designed such that all there is to the contribution process is to suply a name and a version to `ContributeRecipe`:

```
# cd into /Data/Compile/Recipes if you haven't already
sudo ContributeRecipe ExampleRecipe 0.0.1
```

**NOTE:** Please ensure that you use a GitHub account where your name/alias and e-mail address has been added as a **verified GitHub identity** when using `ContributeRecipe`.

`ContributeRecipe` will prompt for your GitHub username and password a couple of times, do its magic and the end result will be a nice GoboLinux GitHub Pull Request which will hopefully get merged.

### Configure `hub` to use `GITHUB_TOKEN` for authentication

As part of its first run, ContributeRecipe will call both `git` and `hub` (`hub` is used to interface with the GitHub API).  During this first run, `hub` will create a GitHub API token and save it in `~/.config/hub`.

Note that, if you have 2-Factor Authentication (2FA) enabled, `git` and `hub` expect you to supply the oauth token that was saved in `~/.config/hub` and NOT your normal password when authenticating.

For convenience, `hub` can be set up to re-use this token for authentication with your GitHub account by exporting the environment variable `GITHUB_TOKEN` in your shell's configuration file (by default, this is `~/.zshrc`):

``` bash
export GITHUB_USER="<the value of your github username>"
export GITHUB_TOKEN="<the value of oauth_token in ~/.config/hub>"
```

To verify that `GITHUB_TOKEN` works as expected, this example might prove useful:

``` bash
. ~/.zshrc
echo "${GITHUB_TOKEN}"
echo "My first gist sent via hub" | hub gist create
```

### How to recover from GitHub login failures

If something goes awry during a `ContributeRecipe` run, you might need to delete the remote branch for subsequent `ContributeRecipe` attempts to be successful.

Once you know the name of the branch that was created, it's as simple as firing off a `git push <remote> --delete <branch>` command.  

Typically, for remote branches the necessary command will look something like `git push origin-fork --delete submit-<recipe>-<version>`.

#### Example:

`git push origin-fork --delete submit-Python-2.7.18`