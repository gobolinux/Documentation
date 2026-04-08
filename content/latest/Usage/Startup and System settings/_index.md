---
title: "Startup & System Settings"
weight: 3
---

> Since we felt like we were "starting from scratch" and we really
> wanted to make a system where everything just made sense for us, we
> also took the time to rethink the boot scripts. I felt the two
> historical models (System V and BSD) were overkill for our common
> desktop-machine setup. GoboLinux uses a simpler system: two scripts,
> `Init` and `Done`, do most of the job. Additional scripts, such as
> `Multi` and `Single`, take care of the runlevels. These files are
> simply sequences of commands, prepended by the word `Exec` and a
> message string.  Here's an excerpt of `Init`:
> 
> ```fish
> Exec "Setting clock..." SetClock
> Exec "Loading keymap..." loadkeys "$KeymapLayout"
> Exec "Bringing up the loopback interface..." ifconfig lo 127.0.0.1
> ```
> 
> More elaborate tasks such as `SetClock` are defined as shell functions
> in a `Tasks` file (these tasks can also be called from the
> command-line using the `RunTask` script). Configurable settings are
> defined as environment variables in the `Options` file. The wrapper
> function `Exec` allows for a nifty additional feature: boot themes.
> The boot sequence can look Slackware-like (with the standard
> error/output messages), RedHat-like (with lots of OK's), or 
> [GoboLinux-like](https://gobolinux.org/k5.html)  (the latter uses a
> modified version of the  [Linux Progress
> Patch](http://lpp-themes.sourceforge.net/)).
>
> ---
> --- Hisham Muhammad, 2003. Excerpt from ["The Unix tree rethought: an introduction to GoboLinux"](https://gobolinux.org/k5.html).

{{% children depth="2" %}}
