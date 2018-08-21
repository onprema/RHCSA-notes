## Install and Update Software Packages from Red Hat Network, a Remote Repository or the Local File System: YUM

Yellowdog Updater Modified (`yum`) is the package manager used in RHEL7, CentOS,
Fedora.

`yum` downloads the `rpm` files and installs them for us. It helps us manage
packages and _dependencies_.

When we install a package with `yum` it will install the dependencies, too. When
we remove a package it will remove the dependencies that were installed during
the original installation.

`yum check-update` looks for any packages that has an update available. `yum
update` will update the packages, but **we don't always want to blindly update
every package** so we can use `yum check-update`.

`yum search apache` only searches the package details and description for
anything that matches the pattern "apache" (case insensitive). We can use
regular expressions and wildcards here, too.

`yum search all apache` looks in the package name, summary, package description,
and package details, and URLs.

`yum info httpd` gives detailed information about the `httpd` package.

By default, we are using the Red Hat authorized repositories and searching for
packages in those repos. Red Hat does a great job of keeping packages in their
repositories security (updating them with patches, etc).

`yum list installed` lists all of the installed packages on the system.
`yum list installed httpd` lists the httpd package (if it's installed).

When you install a package, like `httpd` it will likely create directories and
files on your system. For instance, `/var/www/`. If you want to find out what
package created these directories/files you can use `yum provides /var/www` to
find out what package is responsible for creating those files.

`yum list all` shows a list of _all_ packages available in our repository and
all packages installed on the system.

`yum remove httpd` will remove the httpd package, but the dependencies will
remain on the system.

`yum clean all` removes caching, repos and temporary files associated with yum.
