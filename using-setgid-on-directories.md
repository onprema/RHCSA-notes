## Using set-GID On Directories 

Why would we want to `setgid` on a directory?

It means that whenever new files are created in that directory, those files will
inherit the group owernship of that _parent_ directory.

Usually, when a user creates a file, the group owner is the group the user was
logged in to. (If we weren't using `newgrp`, it is the user's primary group).

`chmod g+s DIR` sets the `setgid` permission bit on DIR. This means that group
owernship for _files within DIR/_ will be the same group owernship as `DIR/`
itself!
