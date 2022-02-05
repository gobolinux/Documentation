---
title: "Configuring the boot process"
menuTitle: "Startup and system settings"
weight: 7
---

This page describes the boot process and how to configure your GoboLinux
system by editing the configuration files used for startup.

## General architecture

The [BootDriver](/Commands/BootDriver/) script
(`/Programs/BootScript/`<version>`/bin/BootDriver`) manages boot-related
tasks. The `init` program (from the Sysvinit package) running as `PID 1`
calls BootDriver as specified in `/System/Settings/inittab`.

[BootDriver](/Commands/BootDriver/) first loads the [boot theme
file](/Documentation/Boot-Themes/) specified in
`/System/Settings/BootOptions`. Then BootDriver runs the appropriate
boot script for the task at hand (startup, shutdown, etc.)

## Boot Scripts

GoboLinux boot scripts initialize and configure the system, manage
daemons, and perform shutdown. They are located at
`/System/Settings/BootScripts`.

-   **BootUp**, the primary startup script, is invoked when you turn on
    the power and the system boots. It contains generic initializations
    common to most Linux systems. Additional scripts are provided to
    support particular boot scenarios.
    -   **Console** runs BootUp and performs initializations required
        for a console session.
    -   **Graphic** runs BootUp and starts X to provide a login window.
-   **Shutdown** is the primary shutdown script, analogous to BootUp. It
    is used by the following termination scripts:
    -   **Reboot** runs Shutdown to terminate system services then
        reboots the machine.
    -   **Halt** runs Shutdown and turns off the power, if possible.
        Otherwise it halts the processor.

Each of these scripts contains lines of the form:

```shell
Exec "Message..." SomeCommand [ parameters ]
```

For example, to adjust the keyboard delay and repeat rate in the
console, you can add this line to
`/System/Settings/BootScripts/Console`:

```shell
Exec "Making keyboard speedy..." kbdrate -r 30 -d 250
```

GoboLinux also provides ["boot tasks"](/Documentation/Boot-script-tasks/) as
a more sophisticated way of managing services.

## Configuration options

When GoboLinux boots, the boot scripts launch programs to configure the
keyboard, set the system clock, initialize the network, etc.

The parameters for calling these programs are placed in
`/System/Settings/BootOptions` and `/System/Settings/NetworkOptions`.
Both files contain entries of the form:

```
Option=value
```

Note that no space is allowed before or after the `=` character. This is
shell syntax, allowing the options to be imported into the boot scripts
using the `source` command.

The following sections document options available in
`/System/Settings/BootOptions` and `/System/Settings/NetworkOptions`.

### Clock mode

GoboLinux needs to know if your hardware clock is set to GMT or local
time. Specify this by editing the ClockMode option. Set `ClockMode=GMT`
if your hardware clock is set to GMT. Set `ClockMode=LocalTime` if your
hardware clock is set to local time.

For obtaining time zone information, Linux applications rely on
information provided by Glibc, the C library. Glibc, on its turn, uses
the `localtime` symlink in its Settings directory
(`/Programs/Glibc/Settings/localtime`) to indicate the active time zone.
This symlink is created by the installer according to the time zone you
selected. You can set this setting manually, by pointing the `localtime`
symlink to a different file under
`/Programs/Glibc/Current/Shared/zoneinfo`.

The ClockMode information is used for the hwclock utility, which is
launched at boot time through the SetClock task.

### Console setup

#### Fonts

Fonts in GoboLinux are stored under `/System/Index/share/consolefonts`
and `/System/Index/share/fonts`. They provide character typefaces for
the Linux console, the X Window System, and `ghostscript`, the Linux
postscript interpreter.

Font path configuration for X can be found in
`/System/Settings/X11/xorg.conf` and
`/System/Settings/fonts/fonts.conf`.

To change the default console font used by GoboLinux, use the
ConsoleFont option in `/System/Settings/BootOptions`.

You can also change the console font using the `setfont` utility. See
`man setfont` for details.

Remember that this setting changes only the console font. On X,
applications have their own font settings.

#### Keymap

Use the KeymapLayout option in `/System/Settings/BootOptions` to select
an appropriate console keyboard layout.

The available keymaps are in the KBD package; they are the .map files.
You can set the console keyboard layout at any time by running loadkeys.
For example, to set the Dvorak keymap, just type in:

`loadkeys dvorak.map`

#### Mouse

The MouseType and MouseDevice options in
`/System/Settings/BootScripts/BootUp` configure mouse support on the
console. They are disabled by default.

### Graphical display setup (X server)

#### Keymap

The keyboard layout for programs running under the window manager is
mapped according the `InputDevice` section in
`/System/Settings/xorg.conf` when the graphic display (X server) starts.
With the window manager running, you can change keyboard mappings and
display settings using `setxkbmap`, `xmodmap`, and `xset` tools. To
select a Dvorak keyboard layout, type `setxkbmap dvorak` in a terminal.
These commands can also be placed in `$HOME/.xinitrc`.

Some desktop environments also offer graphical tools for setting the
keyboard layout. For example, in KDE you can configure this at the KDE
Control Center.

#### Mouse

The mouse pointer for the graphical display is defined in an
`InputDevice` section in `/System/Settings/xorg.conf`. The
[Installer](/Commands/Installer/) should correctly detect your hardware
and set suitable defaults for your system. If not, you can always try a
failsafe setup such as:

```shell
Section "InputDevice"
Identifier  "Mouse0"
Driver      "mouse"
Option      "Protocol" "auto"
Option      "Device" "/dev/input/mice"
Option      "ZAxisMapping" "4 5"
EndSection
```

There is nothing GoboLinux-specific about mouse setup on X. You can find
HOWTOs and tutorials around the net that can give you more detailed
instructions about this. (But feel free to drop by at the mailing list
if you're still stuck!)

### Kernel modules

Through the use of Udev, GoboLinux is capable of loading kernel modules
(e.g. device drivers) automatically at boot. In cases Udev doesn't load
some wanted drivers, the user can explicitly request them.

One way is to edit `/System/Settings/modprobe.conf` (similar to other
Linux distributions), however a simpler way in GoboLinux is to list
desired modules in `/System/Settings/BootOptions`. This is how to load
the i810\_audio audio driver and sk98lin ethernet driver:

```
UserDefinedModules=(
    "i810_audio"
    "sk98lin"
)
```

The startup scripts read this array and run modprobe each line. The
entries may include additional parameters.

### Network configuration

#### Wi-Fi

If you are using Wi-Fi, just select your network using the
[GoboNet](http://github.com/gobolinux/GoboNet) widget in the AwesomeWM
system tray:

<https://gobolinux.org/images/gobo016gobonet.png>

#### Wired network

If you have a wired network, initialize it on boot using standard Linux
commands in your bootscripts sequence.

First, check which are your network interfaces typing

```
ifconfig
```

You should have a network interface named something like `eth0` or
`enp0s3`.

Edit the `/System/Settings/BootScripts/BootUp` script. If you are using
DHCP, just add this:

```
dhcpcd eth0 &
```

If you have a static network configuration, place commands similar to
the following in BootUp.

```
ifconfig eth0 192.168.1.5 netmask 255.255.255.0
route add default gateway 192.168.1.1 metric 1 dev eth0
```

The nameserver can be specified in `/etc/resolv.conf`
(`/System/Settings/resolv.conf`). To use Google's nameservers, you can
edit resolv.conf to:

```
nameserver 8.8.8.8  
nameserver 8.8.4.4
```

### Automated login

If you wish to use an automated login, there are several ways to achieve
this goal.

For KDE (or KDM, it also has a configuration which allows you to tweak
it a lot) you can use this:

1.  Open Control Center in administrative mode.
2.  Select Login Manager.
3.  Under the Convenience tab check "Enable auto-login" and select
    which\_user you should log in as.
4.  Click "Apply".

If you do not use KDE or want a non-GUI based solution, one way is to
use rungetty.

1.  In your inittab file (for example, `nano /etc/inittab`) find the
    line which includes `tty1` (it's your first terminal, the default
    showing up on login).
2.  Now, you will see `agetty` in there - change this `agetty` line to
    `rungetty tty1 --autologin your_username`.

Of course, replace your\_username with the user you want to login as.

Using another tty than 1 may be useful too.

## Printers

GoboLinux comes with CUPS installed by default.

## Audio

Note that ALSA is muted by default, to automatically save and restore
changes done in e.g. alsamixer, add these lines to your boot scripts.

```shell
Done: Exec "Storing ALSA settings..."
alsactl store
```