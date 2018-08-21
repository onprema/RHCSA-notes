## Install and Update Software Packages from Red Hat Network, a Remote Repository or the Local File System: Configuring a Local Repository: Configure the GPG Key

How do you know a package is actually authentic? And its not a
man-in-the-middle, ya know?

GPG keys let us take a public key and verify it against the GPG key in the repo
for the package. So when we download the package it ensures that it comes from
the repo and belongs there.

This is often required for security purposes.

Example: `https://dl.fedoraproject.org/pub/epel/7/x86_64/`

That is the URL for the Fedora EPEL repository.

`yum-config-manager --add-repo https://dl.fedoraproject.org/pub/epel/7/x86_64/`
registers the 3rd party repo with `yum`.

Now what we need to do is **get the public GPG key from the repo** and then
**configure our repository to _use_ that GPG key**.

The GPG keys for the epel repo can be found at
`https://dl.fedoraproject.org/pub/epel/`

The one for RHEL7 is here:
`https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7`

This is the key that verifies that packages from this repository are authentic.

Look inside `/etc/pki` for public/private key infrastructure files.
`/etc/pki/rpm-gpg/` holds the GPG keys for the repos on our system.
