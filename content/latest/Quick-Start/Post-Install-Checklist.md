---
title: Post-Install Checklist
weight: 4
---

##  Your first steps Post-Install:

### 1. Update Compile & Scripts

`Compile` and `Scripts` are our main system tools and are quickly evolving...

Please make sure to update your copies by
running the following commands after you boot into your installed system for the
first time:

```fish
cd /Programs/Scripts/Current
git pull && UpdateSettings --auto Scripts && make
```

```fish
cd /Programs/Compile/Current
git pull && UpdateSettings --auto Compile
```

### 2. Consult "Known issues & fixes"

Refer to our [Known Issues and Fixes]({{%relref "GoboLinux-Known-Issues-and-Fixes" %}}) section
and make sure you handle any issues or errata *before* commencing any significant work, issuing support requests or bug-reporting.

### 3. Set-up Configuration files
Set-up and acquaint yourself with our [configuration files]({{%relref "Configuration-files" %}}).