## Introduction to SELinux

SELinux was originally developed by the NSA (National Security Agency). Red Hat
is utilizing SELinux and it's enabled by default.

In a production environment it's never encouraged to disable SELinux.

If a service like `httpd` has a vulnerability and someone gets access to our
system, they could potentially "become" the apache user and therefore have
access to any files that the apache user can RWX.

If that happens, we are only protected by our file/group permissions and ACLs.

SELinx present a new layer of security.

Processes, files, ports have a _SELinux context_. SELinux determines if a
specific process has permissions to edit or communicate with other resources on
our system.

For example, `httpd` has a default directory of `/var/www/`, owned by the
`apache` user. 

There is a default SELinux context that is created and assigned to all dirs
within `/var/www/`. If there is not an SELinux context set up for a directory
for the `apache` user, it will **not** have access to those files,
**regardless** of file permissions. So if we wanted to serve something from
`/var/webstuff` and we give permissions for the `apache` user to rwx those
files, it won't be allowed to because the SELinux context limits access to
`/var/www/`.

SELinux has three modes:
- Enabled: SELinux is running and enforcing restrictions.
- Passive: SELinux is monitoring and reporting any infringements.
- Disabled: must be configured in `/etc/selinux/config` and a reboot is required
  in order to enter disabled mode.

Passive mode should be used for testing only. Disabled should never be set.

A SELinux **boolean** is a runtime configuration of a security policy without
having to load a new policy. (See `man Booleans`, `man Selinux`, `man Getsebool`).
