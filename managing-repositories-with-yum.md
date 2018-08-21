## Install and Update Software Packages from Red Hat Network, a Remote Repository or the Local File System: Managing Repositories

When you purchase RHEL7 you get access to their official repositories. This is a
premium because Red Hat maintains updates (security updates) very well.

There are 3rd party repos that have packages that may not be supported by Red
Hat. They may not be available inside a Red Hat repository.

One of them is the `epel` repository, managed by the Fedora project.

`yum` repository configuration files are in `/etc/yum.repos.d/`. These files
_must_ end in .repo in order for them to work with `yum`.

Packages that are added to a Red Hat repository (and others) are signed with a
certificate, which is basically a public key used to encrypt and decrypt files.
This is the **GPG key**.

When we download a package we need to have the GPG key that corresponds with the
repository's certificate. This ensures that we are downloading the appropriate
package, safely.

If we are going to download packages from a 3rd party, like `epel` we need to
add their GPG key to our system.

`yum repolist` shows the _enabled_ repositories that `yum` searches through.

`https://dl.fedoraproject.org/pub/epel/7/x86_64/` is the location of an `epel`
repository. If you go there in a browser you'll see directories and the .rpm
packages in the subdirectories.

We can add this repository to our system by using `yum-config-manager
--add-repo=https://dl.fedoraproject.org/pub/epel/7/x86_64/`. This will create a
.repo file in `/etc/yum.repos.d/` and now we can use `yum` to install packages
from this repo.

Note: **If you forget the `yum-config-manager` command, user `apropos yum`**
because it's not in the yum man page!

If we want to disable a repo, we need the name (defined in the .repo file, in
brackets). We can go into that .repo file in `/etc/yum.repos/d` and set the
`enabled=1` to `enabled=0`. You could also do `yum-config-manager --disable
REPO_NAME`. (And `--enable` to re-enable)

You could also just straight up remove the .repo file.
