---
title: "Running under VMWare Workstation Player"
menuTitle: "VMWare Workstation Player"
weight: 3
---

When you install GoboLinux 016 on VMWare and boot it for the first time, you will get a black screen after the GRUB boot selection menu. The underlying problem is that the VMWare SCSI hard disk controller driver has been built as a module on the kernel. Because of that, the virtual disk image is not recognized and booting the installed system fails.

### Workaround

VMWare saves the virtual machine settings on a file with the `.vmx` extension. If you have named your virtual machine "GoboLinux 016", then you will have a file called `GoboLinux 016.vmx`. Shut down VMWare, open that file with a text editor and replace the lines:

```
scsi0:1.present = "TRUE"
scsi0:1.fileName = "GoboLinux 016.vmdk"
scsi0:1.redo = ""
```

with the following:
```
sata0:1.present = "TRUE"
sata0:1.fileName = "GoboLinux 016.vmdk"
sata0:1.deviceType = "disk"
```

The fileName may look different on your machine. You will want to keep whatever name your config file presents.
Also, make sure that the following lines do exist in the vmx file (again, pciSlotNumber may look different on your vmx file):

```
sata0.present = "TRUE"
sata0.pciSlotNumber = "37"
```

Once you are done, save the file and launch VMWare. The system should boot up nicely this time.