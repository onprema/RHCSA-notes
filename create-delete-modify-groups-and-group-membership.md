## Create, Delete, and Modify Local Groups and Group Memberships

`/etc/group` shows all the groups on the system and who is in them.

`getent` is a nice command to use, too. You can do `getent group user` to query
the group db and show what groups `user` is part of. Check out `getent --help`
for more cool stuff.

**get** **ent**ry.

`groupadd` to create a group.

`groupd USER` also shows what groups USER is associated with.

You can change a user's primary group using `usermod -g GROUP USER`

`usermod -aG GROUP USER` **a**ppends a supplementary group to USER's groups.

**User's will need to `exec bash` or logout then login again in order for group
changes to take effect!**

Sometimes you will have a directory that multiple user's share, and you want
them all to be and to RWX the files in that directory. The problem is, with
default `umask`, only the OWNER will have RW permissions.

`newgrp GROUP` lets users log in to a new group (if they are part of GROUP).

**Primary Group** is the group you log in to.
**Supplementary Group** is one you can switch to using `newgroup`.

`groupmod` modifies groups (change name, id, password...)

`groupdel` lets you delete groups, **unless its a primary group of a user**.
