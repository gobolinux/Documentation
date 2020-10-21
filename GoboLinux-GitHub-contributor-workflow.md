This page is intended to document the workflow from setting up Compile.conf for proper attribution, to Compiling and testing a package, to creating a commit with a good commit message to finally submitting a GitHub Pull Request (PR).

## Compile.conf and attribution

Fire up your favourite editor, open `/Programs/Compile/Settings/Compile/Compile.conf` and edit the `compileRecipeAuthor` key as appropriate:

```
# set up proper attribution for GitHub pull requests
compileRecipeAuthor="A. Random Contributor <somebody@some-email-address>"
```

If you are not comfortable using your real name, using a nick/alias is also acceptable.

##