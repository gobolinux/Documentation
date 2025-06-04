---
title: "Getting the Source"
weight: 1
---

Source archives may be downloaded from static urls or from various version
control systems. In the case of a static **url**, a **size** and **md5sum** should be
included for verification.

The following Recipe options control this phase - all
these options are valid for all recipe types:

## Static URLs

#### `url=<url>`

*Note:*

For Sourceforge URLs, use the variable `$httpSourceforge`, as in

```fish
url=$httpSourceforge/<project name>;/<filename>;
```

*Example:*

```fish
url=$httpSourceforge/xmule/xmule-1.8.2.tar.bz2
```

Similarly, use `$ftpGnu`, and `$ftpAlphaGnu`, for downloads from GNU's ftp
servers.

#### `urls=(<array of urls>)`

If the Program has multiple source packages, you may specify a list of them. If
a partial file exists, resumption is attempted. FTP transfers are always
performed in passive mode.

#### `mirror_url=<url>`

#### `mirror_urls=(<array of urls>)`

URLs to be used, in case the URLs listed in `url`/`urls` fail. Multiple mirrors
may be specified. For sets of URLs, each mirror needs to specify the same number
of URLs.

*Example:*

```fish
urls=(
   "http://www.main-site.org/file1"
   "http://www.main-site.org/file2"
)
mirror_urls=(
   "http://www.mirror1.org/file1"
   "http://www.mirror1.org/file2"
   "http://www.mirror2.org/file1"
   "http://www.mirror2.org/file2"
)
```

#### `file=<filename>`

#### `files=(<array of filenames>)`

The name of the package file containing the program's sources. If not specified,
it is assumed to be the same as the final part of the URL, after the last slash.
If `urls` is used instead of `url`, `files` is expected to contain the same
number of entries as `urls`. All of them are unpacked relative to the same
directory by default. To change this behaviour see [unpack_files](#unpack_files)
below.

#### `file_size=<size>`

#### `file_sizes=(<array of sizes>)`

This is the file size(s), in bytes, of the packed archive(s) (e.g. foo.tar.gz)
as reported by `ls -l`.

```fish
user@gobo /Data/Compile/Archives]ls -l gettext-0.16.1.tar.gz
-rw-r--r-- 1 root root 8539634 Jul 11 01:08 gettext-0.16.1.tar.gz
```

#### `file_md5=<md5sum>`

#### `file_md5s=(<array of md5sums>)`

This value contains the [MD5Sum](http://en.wikipedia.org/wiki/MD5) of the
package file defined by the `file` value. You can find this MD5Sum by using the
`md5sum` command.

```fish
user@gobo /Data/Compile/Archives]md5sum gettext-0.16.1.tar.gz
3d9ad24301c6d6b17ec30704a13fe127  gettext-0.16.1.tar.gz
```

## Version Control Systems

#### `cvs=<CVS server>`

#### `cvss=(<array of CVS servers>)`

Specify the CVS server and repository to be used. Note that `cvs`, `svn` and
`url` are mutually exclusive, since you should be either fetching from SCM or
getting a tarball.

*Example:*

```fish
cvs=:pserver:anonymous:@anoncvs.gimp.org:/cvs/gnome
```

#### ``cvs_module=<module name to checkout>``

#### ``cvs_modules=(<array of module names to checkout>)``

CVS module to be checked out.

*Example:*

```fish
cvs_module=gimp
```

#### ``cvs_opts=<string added to cvs operation>``

#### ``cvs_options=<string added to cvs operation>``

Some server configurations require additional options to be passed to the cvs
command. You shouldn't normally need this command, but it is available in case
the documentation of the project you're checking out instructs you to give
special options to cvs.

`cvs_options` is a synonym to `cvs_opts`.

#### `cvs_password=<password>`

Password to log into the cvs server.

#### `cvs_checkout_options=<string added to cvs checkout operation>`

Some configurations require additional options to be passed specifically to the
cvs checkout command, such as for getting a snapshot from a specific date.
Normally, you shouldn't need this command.

#### `cvs_rsh=<string>`

Specify a value for the CVS_RSH variable (see cvs documentation for details). If
unset, `ssh` is used by default.

#### `svn=<SVN server>`

#### `svns=(<array of SVN servers>)`

Specify the Subversion server and repository to be used. Note that `cvs`, `svn`
and `url` are mutually exclusive, since you should be either fetching from a SCM
or getting a tarball.

*Example:*

```fish
svn=http://svn.apache.org/repos/asf/httpd/httpd/branches/2.2.x
```

#### `git=<git server>`

#### `gits=(<array of git servers>)`

#### `hg=<mercurial server>`

#### `hgs=(<array of mercurial servers>)`

#### `bzr=<bazaar server>`

#### `bzrs=(<array of bazaar servers>)`


Similarly, specify an URL for checkout from a Git, Mercurial, Bazaar server,
respectively.
