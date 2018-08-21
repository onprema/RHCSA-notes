## Install and Update Software Packages from Red Hat Network, a Remote Repository or the Local File System: RPM

`rpm` (RPM Package Manager) integrates with `yum`.

`yumdownloader nano` downloads the nano .rpm package from the yum repository.
Note: this downloads the .rpm file, it doesn't install the package.

`rpm -i nano-2.3.1.rpm` will install the package.
`rpm -ivh nano-2.3.1.rpm` (`-h` for hash, which shows a progress bar).

**-q for Query**

`rpm -qa` lists all installed .rpm packages on the system

`rpm -ql nano` lists all the _files_ that were installed with the nano package.
**Very powerful!!**

Query documentation associated with a package `rpm -qd PACKAGE`. Again, **very
powerful!!**

`rpm -e nano` will remove the nano package.

`yum localinstall nano-2.3.1.rpm` installs the package (assuming you have
`nano-2.3.1.rpm` in your CWD) with `yum`.

`yum` is kinda like a wrapper around `rpm`.
