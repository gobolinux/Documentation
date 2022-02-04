---
title: "Set external mailto handler in Firefox"
menuTitle: "External Firefox mailto handler"
---

If you use Firefox and are not running it in KDE or Gnome you'll often
times find that mailto: links don't always or never get handled the way
you would like. If you're interested in setting Firefox to handle
mailto: links with an external program of any kind, here is how you do
it:

1.  Open Firefox
2.  In the address bar go to the page "<about:config>"
3.  First look for the value of
    **network.protocol-handler.expose.mailto** and set it to *true*
    1.  If the value doesn't exists right-click and under "New" choose
        Boolean, then set the name and value to *true*
4.  Second look for the value of **network.protocol-handler.app.mailto**
    and set it to the application you want handling your mail.
    1.  As with the previous value, if it doesn't exist: right-click and
        under "New" choose String, then set it to the value of the
        application you want handling mail.
    2.  ex. /System/Index/bin/xmail

#### Notes

Some useful ways of using this method is to establish a script to launch
a web service as your default means of sending email. A simple script to
handle that would be:

*for the gmail service*

    . GoboPath 
    TO=$(echo $1 | sed 's/mailto://') 
    URL="https://mail.google.com/mail?view=cm&tf=0&to=${TO}" 
