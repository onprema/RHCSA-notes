## Create and Manage Access Control Lists (ACLs)

Not all file systems support Access Control Lists. xfs natively supports it.

`setfacl` allows us to set the ACL on a specific file/dir.
`getfacl` displays the ACL on a specific file/dir.

Examples:
`setfacl -m u:john:rw file1` gives the user "john" rw permissions on file1. Even
if "john" changes its username, it will still have rw permissions.
`setfacl -m m::r file1` sets the mask to r permissions on file1.
`setfacl -m m::- file1` sets the mask to --- on file1.

When you set an ACL you will see a `+` at the end of the permission bits when
you do `ls`. For example: `-rw-r--r--+`.

`chmod` changes the _mask_, not necessarily the permissions for a given user.

You can set the default ACL on a directory. It doesn't change the permissions of
the directory itself, but it sets the default for all files and subdirectories
within it.

For example, `setacl -d -m u:john:rwx dir1` means that user "john" will be able
to read, write and/or execute any file or subdir inside `dir1/`. **But "john"
will need to have permissions to read/write/exec on `dir1/` too!** Not sure
about this...

You can copy the ACL of one file to another by doing `getfacl file1 | setfacl
--set-file=- file2`. Note: the `-` represents stdin.

Note: when it comes to using `setfacl` or `chmod`, `x` means executable
permissions on all files and directories, and `X` means executable permissions
on directories only. Its good practice (more secure) to use `X` in most cases.

Don't forget about the `-R` (recursive) flag on `chmod`. For example, 
`chmod -R g+rwX /tmp` will make all subdirectories in `/tmp` executable for the
group owners.

Note: `cp` does not preserve ACL rules, but `mv` does.
