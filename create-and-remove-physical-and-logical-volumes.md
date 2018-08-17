## Create and Remove Physical Volumes, Assign Physical Volumes to Volume Groups and Create and Delete Logical Volumes
- LVM (Logical Volume Manager)
- Each LVM has an underlying physical storage unit.
- A physical volume can be a partition or entire disk.
- The advantange of using LVM is to be able to expand a disk without having to
  reformat the disk and/or create new partitions.
- LVM is a virtual layer on top of physical storage device(s).
- It's like creating your own SAN (storage area network)
- A **volume group** is a group of physical devices that the LVM uses as a pool
  of resources. Its made up of extents -- the smallest unit of space that can be
assigned to a volume group.

In order to use LVM you need to create a file system and label it as LVM. The
partitions must be `Linux LVM` partitions, which is set using `gdisk` or
`fdisk`.

How do you create a physical volume for the LVM? `pvcreate`. If you want to see
all the physical volumes available to LVM use `pvdisplay`.

Now we need to create a **volume group** by using `vgcreate`. Verify with
`vgdisplay`. You can have multiple volume groups on one system.

Now we can create the LVM by using `lvcreate`. You can specify the LVM in
physical extents (pe) or volume group size (vg). Verify with `lvdisplay`.

Now we can create and mount file systems on these volumes using `mkfs`, then
mount it to the path of the logical volume.

`lvremove` to remove a logical volume.
`vgremove` and `pvremove` to remove volume groups and physical volumes.
