---
title: "Managing Alien Packages"
weight: 6
---

## Introduction

For an introduction to Alien packages please refer to [**Alien Packaging Subsystem**]({{%relref "Alien-Packaging-Subsystem" %}}).

## How to install and update Alien packages

In order to install a foreign package we can use the following syntax:

```fish
sudo Alien --install <package_manager>:<package_name>
```

For instance, in order to install or update meson you would type:

```fish
sudo Alien --install pip3:meson
```