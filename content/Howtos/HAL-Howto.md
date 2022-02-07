---
title: "HAL Howto"
---

With [HAL](http://freedesktop.org/wiki/Software/hal) and
[Ivman](http://ivman.sf.net) and [pmount](http://www.piware.de/projects.shtml),
you can have devices like CD-ROMs and USB flash sticks be automatically mounted
and added to your panel or desktop. When you unmount it the mountpoint will be
removed from your panel.

-   **HAL** is a hardware abstraction layer that keeps track of your hardware,
    both internal and removable. It's like a database that adds information from
    the hardware and from .fdi files, and it can also call other programs when
    certain events happens.
-   **Udev** tells HAL when hardware is added or removed and replaces _Hotplug_
    in this functionality.
-   **Ivman** is a volume manager that can be set up to automount removable
    media, and to do all kinds of other stuff. It reacts when media is inserted
    or removed, or when a property of any device is changed.
-   **Dbus** is an IPC service that lets all these components communicate with
    each other.

NOTE: HAL and Ivman are not limited to storage devices, but also handle stuff
like network cards and other hotpluggable devices on USB, Firewire, PCMCIA,
etc...

## Setup

The following was tried with _Udev 070_, _HAL 0.5.4_, _DBus 0.50_, _Ivman
0.6.4_, and _pmount 0.9.3_. We are going to set things up so that Ivman is run
as root and handles the automounting under `/Mount/Media` , with the help of
pmount. Then users can run their own instances of Ivman too, to handle desktop
specific stuff (like adding devices to the panel).

-   You need to be running Udev and DBus, make sure that's the case and that the
    DBus system bus is started at boot. (Use
    [`StartTask`](/Commands/StartTask)` messagebus`)

<!-- -->

-   You also need a recent kernel and glibc compiled against recent headers.
    This was tested with _Glibc 2.3.5_ with NPTL compiled against
    _Linux-Libc-Headers 2.6.12.0_

<!-- -->

-   Install HAL, Pmount and Ivman:

```fish
] Compile hal
...
] Compile pmount
...
] Compile ivman
...
```

Pmount should be patched with
<http://kymatica.com/stuff/pmount-0.9.3-lijon.patch> and HAL should be patched
with <http://kymatica.com/stuff/hal-0.5.4-lijon.patch> (These patches should be
included with the recipes, together with the small patch that escapes the
$hal.volume.mount\_point$ in ivmans src/manager.c:619)

-   Make sure there is nothing in `/System/Settings/hal/device.d` that does any
    mounting, becouse we want ivman to handle the mounting! (Actually I don't
    think device.d works in HAL 0.5.4 since they moved to `info.callouts.*`
    instead...)

<!-- -->

-   Make sure there is a `haldaemon` system group and user, and a `plugdev`
    group. Add all users that should be able to access and unmount removable
    media to the `plugdev` group. _Note that users must log out and in again for
    the group changes to take effect_

<!-- -->

-   Start HAL as root:

```
] StartTask hald
```

-   Start Ivman as root:

```
] ivman
```

NOTE: If all this works, don't forget to check that hald and ivman is started in
your bootscripts:

```fish
Exec "Starting D-Bus system bus..."             messagebus
Exec "Starting HAL daemon..."                   StartTask hald 
Exec "Starting Volume Manager..."               ivman
```

-   Make sure Ivman is started as your user too: Add this script in your
    AutoStart folder:

```shell
#!/bin/sh
exec 1>&2
echo -n "Launching volume manager... "
if ps -C ivman -o user | grep -q $USER
  then
    echo "Already running."
    exit
  else
    echo "OK"
    exec ivman
fi
```

-   Disable mounting with usermode ivman, or else there will be problems if more
    than one user is logged in and running ivman at the same time... We want the
    root ivman to handle mounting. In `~/.ivman/IvmConfigActions.xml`, comment
    out this section:

## Ivman rules to add devices to your ROX panel

-   Create a script named `~/bin/rox.panelput` and make it executable:

```fish
#!/bin/sh
### Change "Top" below to the panel you want your devices on...
rox --RPC << EOF
<?xml version="1.0"?>
<env:Envelope xmlns:env="http://www.w3.org/2001/12/soap-envelope">
<env:Body xmlns="http://rox.sourceforge.net/SOAP/ROX-Filer">
<Panel$1>
<Side>Top</side>
<Path>$2</path>
</panel$1>
</env:body>
</env:envelope>
EOF
```

-   And here comes the ivman rule, which should be inserted in your
    `~/.ivman/IvmConfigProperties.xml` (this files is created first time you run
    ivman as a user)

```xml
<ivm:Match name="ivm.mountable" value="true">
<ivm:Property name="hal.volume.is_mounted">
<ivm:Action value="true" exec='rox.panelput Add "$hal.volume.mount_point$"' />
<ivm:Action value="false" exec='rox.panelput Remove "$hal.volume.mount_point$"' />
</ivm:property>
</ivm:match>
```

## A nice `~/bin/eject` script:

This lets you unmount your media and also FUSE mountpoints with the _Eject_
entry on the right-click menu on mountpoints. Don't forget to make the script
executable.

```fish
#!/bin/sh
pumount "$1" 2>/dev/null || fusermount -u "$1" 2>/dev/null ||
echo "Could not unmount with pumount or fusermount -u" >&2
```

## More patches

### Spaces in mountpoint names

Ivman 0.6.5 and earlier have the problem that mountpoints are not enclosed by
quotes when passed as arg to `pmount`. So if a inserted media has spaces in the
desired mount point, pmount will fail! look in ivmans `src/manager.c:619` and
put \\" around the `$hal.volume.desired`_`mount`_`point$` thing... This bug was
fixed upstream in Ivman 0.6.6, thus this workaround is no longer required.

### Better mountpoint names

At least for me, my CD-ROM's got mounted as `/media/hde` and stuff like that,
this patch to
`/System/Index/share/hal/fdi/policy/10osvendor/10-storage-policy.fdi` fixed it
so that media is mounted with the volume label as mountpoint:

```patch
-       <match key="@block.storage_device:storage.no_partitions_hint" bool="false">
-
+
<merge key="volume.policy.should_mount" type="bool">true</merge>
<merge key="volume.policy.mount_filesystem" type="copy_property">volume.fstype</merge>

@@ -173,7 +172,7 @@
<merge key="volume.policy.should_mount" type="bool">true</merge>
</match>
</match>
-       </match>
+
</match>
</match>
```

Note that you can put a copy of this file under /System/Settings/hal/fdi/policy
and patch that one instead.

# Making different types of media get different icons

With ROX, it's also possible to have the inserted media get an icon that
represents the type of media inserted.

-   Patch rox-filer to add SOAP calls for setting icons:
    <http://kymatica.com/stuff/rox-2.3-iconsoap.patch>

-   Add this `/System/Settings/hal/fdi/information/10-usb-flash.fdi` to detect
    usb flash sticks:

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <deviceinfo version="0.2">
    <device>
    <match key="@block.storage_device:storage.bus" string="usb">
    <match key="info.category" string="volume">
    <merge key="volume.is_usb_storage" type="bool">true</merge>
    </match>
    </match>
    </device>
    </deviceinfo>
```

-   Change your `~/.ivman/IvmConfigProperties.xml` rule to this:

```xml
<ivm:Match name="hal.volume.is_usb_storage" value="true">
<ivm:Property name="hal.volume.is_mounted">
<ivm:Action value="true" exec='rox.seticon Set "$hal.volume.mount_point$" $HOME/.ivman/usb.png' />
<ivm:Action value="false" exec='rox.seticon Unset "$hal.volume.mount_point$"' />
</ivm:property>
</ivm:match>

<ivm:Match name="hal.volume.is_disc" value="true">
<ivm:Property name="hal.volume.is_mounted">
<ivm:Action value="true" exec='rox.seticon Set "$hal.volume.mount_point$" $HOME/.ivman/cdr.png' />
<ivm:Action value="false" exec='rox.seticon Unset "$hal.volume.mount_point$"' />
</ivm:property>
</ivm:match>

<ivm:Property name="hal.volume.is_mounted">
<ivm:Action value="true" exec='rox.panelput Add "$hal.volume.mount_point$"' />
<ivm:Action value="false" exec='rox.panelput Remove "$hal.volume.mount_point$"' />
</ivm:property>
</ivm:match>
```

-   Create this script in `~/bin/rox.seticon` and make it executable:

```xml
rox --RPC << EOF
<?xml version="1.0"?>
<env:Envelope xmlns:env="http://www.w3.org/2001/12/soap-envelope">
<env:Body xmlns="http://rox.sourceforge.net/SOAP/ROX-Filer">
<$1Icon>
<Path>$2</path>
<Icon>$3</icon>
</$1icon>
</env:body>
</env:envelope>
    EOF
```

-   And put some icons for `other.png`, `cdr.png` and `usb.png` in `~/.ivman/`
    and you're done!
