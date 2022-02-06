---
title: "Fibo"
---

In GoboLinux, `Fibo` is a special user that assists Gobo, the
superuser, during program installation. `Fibo` is
responsible for the [`FiboSandbox`](/Commands/FiboSandbox/), he is the
only one who is given access to it.

Fibo is similar to the Unix `nobody` user, but the
fundamental difference is while `nobody` **never** has write access to
anything, Fibo is occasionally granted write permission to selected
locations (specifically, during program installation, to the
[`FiboSandbox`](/Commands/FiboSandbox/) and to the `/Programs` entry of the
program being installed).

In a standard GoboLinux system, `Fibo` is userid 21 (which is, of
course, a number of the [Fibonacci
sequence](http://en.wikipedia.org/wiki/Fibonacci_sequence)).
