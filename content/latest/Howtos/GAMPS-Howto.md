---
title: "GAMPS Howto"
hidden: true
---

GAMPS is a GoboLinux/Apache/MySql/P/SSL web serving system. This document is
intended to be a step-by-step manual on setting up a MySQL database server and
Apache web server with PHP/Python/Perl/SSL support in GoboLinux.

## MySQL

1. First, you have to install MySQL. Fire up a console and type `Compile mysql`.

Once you've answered Compile's initial wave of questions, you should have enough
time to make yourself some coffee.

-   When the compilation has finished, you may choose a config file to use. The
    mysql configuration is stored in `/Programs/MySQL/Settings/mysql`, and the
    config file actually used has to be named `my.cnf`. The default config file
    is `my-small.cnf`. If you're happy with this, go to the next step; otherwise
    choose one of the other config files and overwrite `my.cnf` with it.
-   Now it's time to start the MySQL server. Do this by typing

```fish
StartTask MySQL
```

{{% notice note %}} If the server crashes at this moment you might want to check
the permissions of `/Data/MySQL`. Owner and group must both be `mysql`. You can
achieve this by typing

and starting the server again. {{% /notice %}}

-   The next step is to set a password for the MySQL root user. Type

```fish
mysqladmin -u root password mYNewpAsSw0rD
```

-   If you want to start the MySQL server automatically at boot time, type

```fish
echo 'Exec "Starting MySQL Database Server..." MySQL Start' \ >> /System/Settings/BootScripts/BootUp
```

-   You can test your MySQL installation by typing

```fish
mysql -u root -p
```

If everything worked, you'll be prompted for a password, then taken to the MySQL
monitor.

## OpenSSL - Part 1

## Apache

-   As usual, compiling is the first step:

```fish
Compile HTTPD
```

-   After compilng, Apache should be ready to start. Just type

```fish
StartTask HTTPD
```

-   If you want to start the Apache server automatically at boot time, type

```fish
echo 'Exec "Starting Apache Web Server..." HTTPD Start' \ >> /System/Settings/BootScripts/BootUp
```

## OpenSSL - Part 2

TODO

## PHP

-   To install Apache PHP Module, type

```fish
Compile Mod_PHP
```

You have to restart Apache to load the new PHP module: `StopTask HTTPD` then
`StartTask HTTPD`.

## Python

Compile the module

```fish
Compile Mod_Python
```

Restart Apache again

`StopTask HTTPD`, `StartTask HTTPD`

If you use HTTPD 2.0.x you have to edit your `httpd.conf`
(`/Programs/HTTPD/Settings/httpd/httpd.conf`) to load the Python module with
Apache. Add the following line after the other `LoadModule` directives:

```fish
LoadModule python_module modules/mod_python.so AddType application/x-python-code pyo pyc AddType text/x-python py
```

## Perl

TODO

## Celebrate!

You're done! All you have to do now is place your websites at
`/Depot/WWW/Documents`
