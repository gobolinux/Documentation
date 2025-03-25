---
title: "GoboLinux-PPC"
---

### A quick note on the PowerPC port

A while ago it was announced on the GoboLinux mailing lists that there was work
ongoing for a PowerPC port. That was a one-man work (by
[hisham](https://hisham.hm/)). It is now fairly complete (my main computer is
now an iBook running GoboLinux) but it not as polished for release as the x86
version.

What's missing:

-   Work on the bootscripts. I was not bothered to do that.
-   Live-CD stuff. It exists only in my HD now.
-   Minor glitches in some packages. There are some problems in a few packages
    (e.g. KDE-Libs) which _I_ can live with fine, but that I know that if I
    release, people wil complain.

So, yeah, it is now at a state where you could call it a "half-a\*\*ed-job", but
it works for me. So, to avoid the flamefests we've seen on the list, I'm not
going to release this until somebody shows up who is willing to work on the
missing parts.

I intend to integrate the changes/additions I did to the recipe store on this
work, though.

That's it for now, have a nice day.
