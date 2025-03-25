---
title: "Boot Script Tasks"
---

Your boot scripts can make use of "boot tasks", which are little service scripts
that can be shipped by programs. A program includes its tasks under
`Resources/Tasks`, and they're linked in `/System/Tasks`. This is roughly
equivalent to the `/etc/init.d` scripts found in many distributions.

You can launch or stop tasks from the command line, using
[`StartTask`]({{%relref "StartTask" %}}) and [`StopTask`]({{%relref "StopTask" %}}).
For example, the following command will load the SSH daemon:

```fish
StartTask OpenSSH
```

Within boot scripts, you don't need to use these launchers, but you have to add
a parameter indicating whether the task is being started or stopped:

```fish
Exec "Initializing OpenSSH server..." OpenSSH Start
```

## Creating tasks

Strictly speaking, a task is simply a shell script put in the appropriate
directory, which accepts `start` and `stop` parameters. In this imaginary
example, one could have a file `/Programs/Foo/1.0/Resources/Tasks/Foo` with
these contents:

```fish
#!/bin/sh

case "$1" in
[Ss]tart)
    # actions to start foo go here
    foo --silly-walk
    ;;
[Ss]top)
    # actions to stop foo go here
    killall foo
    ;;
esac
```

It's a good idea to use the above example as a template for tasks you create.
The `[Ss]` syntax ensures that both `start` and `Start` are recognized, which is
nice to avoid typos.
