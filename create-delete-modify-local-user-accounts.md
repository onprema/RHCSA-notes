## Create, Delete, and Modify Local User Accounts

If you see `/sbin/nologin` on a line in `/etc/passwd` its like saying "if this
user tries to login to a shell; **don't let it**". Like, we don't want `apache`
ssh'ing into our system.

When we create a new user, we also create a new group that is the the same name
as the user's name.

`/etc/skel` - Any files inside here would be copied from this directory into a
new user's home directory! This could be useful for READMEs for new users :)
Note, you could also create a specific _skel_eton directory with `useradd --skel
SKEL_DIR` when you create the new user.

`/etc/login.defs` shows the default options when creating new users.

`/etc/default/useradd` also has the defaults for `useradd`.

`usermod --help` modify user accounts.

"Locking" a user prevents them from logging into the system. It basically
changes the user's password (you'll notice a `!` in front of their encrypted
password in `/etc/shadow`)


