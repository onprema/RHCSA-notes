## Configure Systems to Mount File Systems at Boot by UUID or Label

Labels are helpful for identifying storage devices.

- To label a device with an xfs file system, use `xfs_admin`.
- To label a device with an ext4 file system, use `e2label` or `tune2fs`.

Now that we have labeled our storage devices, let's create persistent mounts for
our system. Currently, if we were to reboot our system and then mount a device
it wouldn't mount automatically (we'd have to do it manually with `mount`).

Note: if you mount a file system, it's **not** persistent. It won't be there
next time to the machine boots up. That's why we are doing this!

In order to create persistent mounts, we need to modify `/etc/fstab`.

`mount -a` attempts to mount all file systems in `/etc/fstab`.
`umount -a` attempts to umount everything in `/etc/fstab`.

Defining the filesystems in `/etc/fstab` makes the mounts persistent. Well,
actually it just mounts them at boot so you don't need to do it manually.
