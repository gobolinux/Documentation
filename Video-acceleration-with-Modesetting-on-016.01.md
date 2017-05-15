GoboLinux 016.01 ships with the xf86-video-modesetting driver overriding the deprecated xf86-video-intel driver. Modesetting is noticeable more stable, but it won't offer video acceleration for 2D operations by default. You'll need to recompile the following packages to achieve Gallium-based 2D acceleration on 016.01 systems:

1. `Compile libdrm`
2. `Compile libva`
3. `Compile intel-vaapi-driver`
4. `Compile mesa`
5. `Compile xorg-server 1.18.4`

Further, you need to modify two Xorg settings files:

1. Edit `/System/Index/share/X11/xorg.conf.d/20-intel.conf` and add an "AccelMethod" entry to the "Device" section:
```
Section "Device"
  Identifier "Intel Graphics"
  Driver     "modesetting"
  Option     "AccelMethod" "glamor"
EndSection
```

2. Edit `/System/Index/share/X11/xorg.conf.d/glamor.conf` so it reads:
```
Section "Module"
    Load  "dri2"
    Load  "dri3"
    Load  "glamoregl"
EndSection
```

Now you should be able to get 2D acceleration the next time you launch the X server.