## List and identify SELinux file and process context

Every file and directory has an SELinux _context_. We can see the context by
doing `ls -Z`. Here is an example:

```
$ cd /var/
$ ls -Z
...
drwxr-xr-x. root root system_u:object_r:httpd_sys_content_t:s0 www
...
```
`httpd_sys_content_t`
- `_t` means its a **type context**.
- `httpd_sys_content` is the **type**. It means that `httpd` has permissions to
  communicate with this dir (`/var/www/`). This is essentially an application
layer firewall.

All the files inside `/var/www/` need to have the `httpd_` context.
```
drwxr-xr-x. root root system_u:object_r:httpd_sys_script_exec_t:s0 cgi-bin
drwxr-xr-x. root root system_u:object_r:httpd_sys_content_t:s0 html
```
`/var/www/cgi-bin` has a `_script_exec` type policy
`/var/www/html` has a `_content` type policy

`semanage` is a tool to configure SELinux policies.

`semanage fcontext -l | grep httpd` shows the httpd contexts

**`ps auxZ` will show the SELinux context for all processes!**

`restorecon FILE` will set the security context for a FILE based on where it is
in the filesystem to the default SELinux settings.

`/.autorelable` is a file in `/` that will configure SELinux to _relable_ every
file on our filesystem when we reboot.
