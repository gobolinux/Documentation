---
title: Post-Install Checklist
weight: 3
---

## First things first

### Update Compile & Scripts

`Compile` and `Scripts` are our main system tools and are always evolving!

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

## Config files
Set-up and acquaint yourself with our [configuration files]({{%relref "Configuration-files" %}}).

## Known issues & fixes

Please make sure to always check out our [Known Issues and Fixes]({{%relref "GoboLinux-Known-Issues-and-Fixes" %}}) section!