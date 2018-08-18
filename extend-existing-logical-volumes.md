## Extend Existing Logical Volumes

`vgextend` extends the logical volume group
`pvmove DEV` moves data from DEV to other physical volumes in a volume group
`vgreduce GROUP DEV` moves DEV from GROUP

This is a way to take out a partition but still keep the data! (now it lives on
another physical volume that is part of the logical group)

- No manual moves
- No losing data
- Virtual storage!

Extend the SIZE of the logical volume
- `lvextend -L 10G /dev/mygroup/myvolume` increases the size of the lv to 10GB
- With xfs, **you must use `xfs_growfs /mnt/mymount` to see changes in `df-h`**
- With ext, you use `resize2fs /mnt/mymount`

BONUS: `lvextend -L +50%FREE /dev/mygroup/myvolume` increases the logical volume
by 50% of it's available space.
