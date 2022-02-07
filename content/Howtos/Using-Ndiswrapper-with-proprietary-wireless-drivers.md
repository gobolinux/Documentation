---
title: "Using Ndiswrapper with Proprietary Wireless Drivers"
menuTitle: "Ndiswrapper & Proprietary WIFI drivers"
---

First of all, my network card is a Broadcom 802.11b/g WLAN pci card built-in in
my laptop P4 Compaq Presario 2568. I didn't found Linux kernel drivers for it,
so I used the drivers of my WinXP installation.

What I needed to have it working was basically:

-   Install the package `WirelessTools`
-   Get the Win drivers for the wireless device and the `.inf` file
    correspondent
-   Install the [ndiswrapper](http://ndiswrapper.sourceforge.net/) program
-   Use `ndiswrapper` to install the driver. This is the easy part, just run:

```fish
ndiswrapper -i DRIVER.inf
ndiswrapper -m
```

as gobo.

-   Use [`WirelessTools`](/Commands/WirelessTools) to configure the interface
    and to find an wireless network available
-   Use ifconfig to open the interface and DHCP to configure the connection.
-   Browse the web

You can automate some of this by adding a line to
`/System/Settings/modprobe.conf` of install wlan0 modprobe ndiswrapper &&
iwconfig wlan0 ... (put your usual commands here, with && between) and then
adding `wlan0` to `/System/Settings/BootOptions` with the right config.
