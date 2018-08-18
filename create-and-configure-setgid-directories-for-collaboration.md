## Create and Configure Set-GID Directories for Collaboration

All files created inside a directory that has the `setgid` bit set on it will
obtain/inherit the permissions of the _parent_ directory.

`setuid` executes the file _as the user who owns the file_, not the user who
executes the file. `setgid` is the same, except for group -- it executes with
the permissions of the group-owner of the file, not of the user-group that
executing the file.

When you `setgid` a directory it enables the inheritance of permissions of the
parent directory to all new files created inside of it.

Note: `setgid` is not a command, but a C function. To set the `setgid` bit you
need to use `chmod g+s` on the file or dir. Same for `setuid` (`chmod u+s`)

Don't forget, to change ownership of a file/dir, use `chown user:group`.

Great, but how does this enable collaboration?

Well, if you have a local user that goes into /finance, for example, and you
don't have the setgid bit on there. The files that the local user creates will
have the ownership of the user and it's primary group. This means that unless
other users _also_ belong to the local user's group, they can't view those
files!
