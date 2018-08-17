## List, Create and Delete Partitions on MBR and GPT Disks
MBR (Master Boot Record) based partitions are limited to 2TiB (2048 GB) and
  there can only be 4 partitions on a single device.

Creating, Deleting MBR Partitions on a device:
- `fdisk` (think **f**ormat disk) manages MBR-based partitions
- Note: all commands in `fdisk` are only done in-memory. In order to make them
  effective you must use `w` to write and exit.

Now that you have a new partition on a disk, what do you do with it?
- To start storing data on it, you need to format it with a file system, such as
  xfs or ext4. RHEL prefers xfs!
- `mkfs` can be used to do that. 
- Once you add an fs to the partition, you need to **mount** it before you can
  write data to it.
- `df -h` will list all the mounted fs's on the system.
- `blkid` will list all the available block storage devices (partitions on a
  disk) that are attached to the system. Only those with file systems attached
to them will be listed.

How do you mount a device?
- Create a location where you want to mount your device to. Best practice is to
  put it in `/mnt`. Make a directory in there.
- `mount /dev/mydevice /mnt/mymount` mounts the file system to that location.
- Note: a "file system" now means (block device + file system)
- `umount` is for unmounting file systems from a device. **This will not delete
  the data that was in written to /mnt/mymount**. The data persists on the block
device (at /dev/mydevice)

Whenever you create or delete a partition you should use `partprobe` to inform
the kernel of the changes.

Devices come with a UUID (universal unique identifier) because devices
technically could have the same name. It's good practice to use the UUID when
mounting file systems to avoid that potential problem.

--------------------------------------------

GPT (GUID Partition Table) based partitions can have 8ZiB (8,000,000 TiB) and
  there can be 128 partitions on a single device.

- `gdisk` is the equivalent of `fdisk` for GPT based partitions. `parted` is
  another command you can do to manipulate partitions, but `gdisk` is more
straight-forward.
- The rest of the commands are pretty much the same.
