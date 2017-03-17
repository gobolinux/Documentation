Here is what you need to do to boot an ISO image of Gobo
under QEMU and install the OS to a disk image on the
host filesystem.

### Create a disk image 

This is where we will install our Linux system.

```
qemu-img create gobo.img 10G
```

### Boot the installer

Here is the command line if you use the helper script
<code>qemust</code> which appears below.

```
qemust --iso=GoboLinux-016.01-alpha-x86_64.iso --image=gobo.img
```

Here is the full command you can edit and past into the
terminal:

```
sudo qemu-system-x86_64 \
-enable-kvm \
-show-cursor \
-boot d -m 768 \
-cpu host -daemonize \
-vga std -soundhw ac97 -rtc base=utc \
-usb -usbdevice tablet -device usb-mouse -vga std -clock unix \
-cdrom GoboLinux-016.01-alpha-x86_64.iso \
-hda gobo.img
```

### Boot the disk image

Shutdown the guest OS after you've finished the
installation.  Start QEMU again, this time booting from the
disk image:

```
qemust  --image=gobo.img
```
The full command is:

```
sudo qemu-system-x86_64 \
-enable-kvm \
-show-cursor \
-boot c -m 768 \
-cpu host -daemonize \
-vga std -soundhw ac97 -rtc base=utc \
-usb -usbdevice tablet -device usb-mouse -vga std -clock unix \
-hda gobo.img

```

## Networking

QEMU provides a networking stack so that the guest OS
running on this virtual machine can access the internet, or
ssh to the host.

The only extra setup needed is to run Gobo's DHCP client
inside the guest. 

```
dhcpcd
```

By default QEMU acts as a firewall and does not permit any
incoming traffic. It also doesn't support protocols other
than TCP and UDP.  This means that ping and other ICMP
utilities won't work.

Details can be found
[here.](https://en.wikibooks.org/wiki/QEMU/Networking#User_mode_networking)

## Qemust

This is a perl5 script that you can run to start your QEMU
process.  Then install the script's dependencies. 
I would suggest using the _cpanminus_ client:

```
cpan App::cpanminus
cpanm Getopt::Long::Descriptive
```

Of course you may want to edit the QEMU parameters to your choice. 
then make the script executable, with something like
<code>chmod a+x ~/bin/qemust</code>.

```
#!/usr/bin/env perl
use strict;
use warnings;

#   qemust - start QEMU

use 5.012;
use Getopt::Long::Descriptive;
my ($opt, $usage) = describe_options(
   '%c %o',
   [ 'iso=s',  "ISO file to boot" ],
   [ 'image=s',"OS disk image file" ],
   [ 'help',   "print usage message and exit" ],
   [ 'n',      "print QEMU startup command and exit" ],
 );
print($usage->text), exit if $opt->{help} or ! keys %$opt;

my $boot_drive = $opt->{iso} ? 'd' : 'c';

my @cmd = grep{! /^\s*$/} map{s/\s*#.*$//; $_} split "\n",<<"CMD";

sudo                 # run as root
qemu-system-x86_64   # for 64-bit CPUs
-enable-kvm          # faster virtualization
-show-cursor         #
-boot $boot_drive    # boot from DVD/CDROM if present
-m 768               # use memory 768MB
-cpu host            # same CPU model as host
-daemonize           # avoid race conditions when QEMU started by external program
-vga std             # probably -vga vmware would work, too
-soundhw ac97        # typical soundcard, -soundhw hda should also work
-rtc base=utc        # timer related
-usb                 # enable USB driver
-usbdevice tablet    # so QEMU can report mouse position without grabbing mouse
-device usb-mouse    # 
-clock unix          # 

CMD

push @cmd, "-cdrom $opt->{iso}" if $opt->{iso};
push @cmd, "-hda $opt->{image}" if $opt->{image};
my $cmd = join " \\\n",@cmd;
say $cmd;
system($cmd) unless $opt->{n};
__END__
```
