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
