## Install and Update Software Packages from Red Hat Network, a Remote Repository or the Local File System: Configuring a Local Repository

Here's a situation: we have a RHEL7.iso installation disk. We want to make a
local repository of the packages on the disk.

How do we mount a .iso file as a block device?

`mount -o loop myfile.iso /my/location` - loop let's it be read as a block device.

Now we can `ls /my/location` and we see the files that are on the .iso!

We can create a file `/etc/yum.repos.d/local-repo.repo` with the following
configuration:
```
[local-repo]
name=Red Hat Linux Local Repo
baseurl=file:///repos/local
enabled=1
gpgcheck=0
```

Now we can do `yum repolist` and we'll see that our local repository has been
registered with yum.
