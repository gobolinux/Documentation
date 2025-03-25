---
title: "Sandbox Install"
---

If I wanted to run make my self, what would I need to do to sandbox it? It would
be useful to know how its done.

```fish
tar xvzf Foo.tar.gz
cd Foo
PrepareProgram Foo 1.0 -- --enable-crazy-feature-x
make
PrepareProgram -t Foo 1.0
SandboxInstall Foo 1.0
SymlinkProgram Foo 1.0
```

Also see [Manual Compile]({{%relref "Manual-Compile" %}})
