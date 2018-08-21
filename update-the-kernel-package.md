## Update the Kernel Package Appropriately to Ensure a Bootable System

Goal: update our kernel manually.

`uname -r` shows the current kernel on your system.

It is not encourage by Red Hat to compile your own kernel. If you do, it's not
considered a Red Hat distro. Instead, they suggest downloading the kernel from
the official Red Hat repo.

`yum upgrade` will update the kernel, if there is an updated version available.

`yum list kernel` will show the currently installed kernel as well as updated
kernels available. You can do `yum clean all` to get rid of stale file, which
may result in displaying the actual newest kernel available.

If there is a newer kernel available you can do `yum update kernel` to install
it on the system. Or you can do it with `rpm`:

`yumdownloader kernel` will download the .rpm package.

`rpm -ivh kernel-3.1.blah.blah` to install. **You might get a dependency
error**. If there are missing dependencies, they will be displayed, then you
just need to install those with `yum`.

If you do `uname -r` after installing the kernel, you'll see that the system is
still running the older one. _But_ you will see the updated kernel files in
`/boot`, which will be the place the system looks next time it boots up, so on
reboot you will have the updated version of the kernel.
