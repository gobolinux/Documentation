---
title: "Package Signing"
---

### QuickStart

First you need to create a pair of GPG keys. A nice GUI tool for this is
KGpg. This is included with recent KDE-Utils.

If you haven't used KGpg before, execing kgpg starts the "KGpg Wizard".
Follow the instructions to generate your key pair. Suggestions for key
length and other properties? I've used the default settings: 1024 and
DSA/ElGamal.

After the wizard, export your public key to a file. Use
"[KeyManager](/Commands/KeyManager/) --import key.asc" to import the
public key to Gobo's system keyring.

Now you can use "[CreatePackage](/Commands/CreatePackage) --sign" and
[SignProgram](/Commands/SignProgram) to create signed packages and
/Programs.

### Overview

Private keys are kept in the users /.gnupg/keyrings. Public keys, used
for verification, are kept in
/Programs/Scripts/Current/Data/gpg/goboring.gpg.

Resources/[FileHash](/Commands/FileHash) is a text file containing the
md5sums for each file.

Resources/FileHash.sig is the gpg signature for
[FileHash](/Commands/FileHash).
