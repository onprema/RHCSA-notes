## Add New Partitions and Logical Volumes and Swap to a System Non-Destructively

Let's make some swap space.

Swap space is **disk space** that the kernel can use as a backup location for
idle memory usage (memory allocated for running programs that are perhaps not
needed immediately).

We can use LVM or a regular device to create swap space.

It's suggested to use about 2 times the amount of available memory. So if you
have 1GB of RAM, you might set up your swap space to be 2GB.

(You can use `free -m` to see how much memory you have [in MB])

> create logical volume using `fdisk`, `pvcreate`, `vgcreate`, `lvcreate`.

After creating a logical volume, we need to prepare it to be our swap space. We
need to give is a "swap signature" by using `mkswap`. This will give us the UUID
of the swap space.

We can use `swapon` to enable swap and `swapoff` to remove it (just like `mount`
and `umount`!). **This is not persistent**.

`swapon -a` is like `mount -a`, it attempts to add any swap disks in `/etc/fstab`.

If we want persistency, we need to modify the `/etc/fstab` file.

**If you are creating a partition for swap space using `fdisk` be sure to set
the correct ID. In this case, "Linux swap"**.
