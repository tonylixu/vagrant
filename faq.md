### Vagrant was unable to mount VirtualBox shared folders. This is usually because the filesystem "vboxsf" is not available.
If you are seeing this error with you try to `vagrant up`, it's probably that you are missing the `vagrant-vbguest` plugin.
```bash
==> default: Mounting shared folders...
    default: /vagrant => C:/devel/new-devbox
Vagrant was unable to mount VirtualBox shared folders. This is usually
because the filesystem "vboxsf" is not available. This filesystem is
made available via the VirtualBox Guest Additions and kernel module.
Please verify that these guest additions are properly installed in the
guest. This is not a bug in Vagrant and is usually caused by a faulty
Vagrant box. For context, the command attempted was:

mount -t vboxsf -o dmode=777,fmode=666,uid=1000,gid=1000 vagrant /vagrant

The error output from the command was:

/sbin/mount.vboxsf: mounting failed with the error: No such device
```
Install the plugin (Make sure you don't have a `Vagrantfile` in your pwd otherwise it may fail due to the your `Vagrantfile`):
```bash
$ vagrant plugin install vagrant-vbguest
```
Then next time when you `vagrant up`, it will fix automatically:
```bash
[default] GuestAdditions versions on your host (5.2.16) and guest (4.3.30) do not match.
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.vwtonline.net
 * epel: archive.linux.duke.edu
 * extras: centos.eecs.wsu.edu
 * ius: archive.linux.duke.edu
 * updates: centos2.zswap.net
Package kernel-devel-3.10.0-862.9.1.el7.x86_64 already installed and latest version
Package kernel-devel-3.10.0-862.9.1.el7.x86_64 already installed and latest version
Package gcc-4.8.5-28.el7_5.1.x86_64 already installed and latest version
Package binutils-2.27-28.base.el7_5.1.x86_64 already installed and latest version
Package 1:make-3.82-23.el7.x86_64 already installed and latest version
Package 4:perl-5.16.3-292.el7.x86_64 already installed and latest version
Package bzip2-1.0.6-13.el7.x86_64 already installed and latest version
Nothing to do
Copy iso file C:\Program Files\Oracle\VirtualBox\VBoxGuestAdditions.iso into the box /tmp/VBoxGuestAdditions.iso
Mounting Virtualbox Guest Additions ISO to: /mnt
mount: /dev/loop0 is write-protected, mounting read-only
Installing Virtualbox Guest Additions 5.2.16 - guest version is 4.3.30
Verifying archive integrity... All good.
Uncompressing VirtualBox 5.2.16 Guest Additions for Linux........
VirtualBox Guest Additions installer
Removing installed version 4.3.30 of VirtualBox Guest Additions...
Copying additional installer modules ...
Installing additional modules ...
VirtualBox Guest Additions: Building the VirtualBox Guest Additions kernel modules.  This may take a while.
VirtualBox Guest Additions: Starting.
Redirecting to /bin/systemctl start vboxadd.service
Unmounting Virtualbox Guest Additions ISO from: /mnt

==> default: Checking for guest additions in VM...
==> default: Setting hostname...
==> default: Mounting shared folders...
    default: /vagrant => C:/devel/new-devbox
    default: /home/vagrant/.ssh => N:/.ssh
```
After you log in your vagrant box, you can see a mount point `vagrant                  239G  187G   52G  79% /vagrant`
