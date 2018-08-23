## Set enforcing and permissive modes for SELinux

When you're setting up a web server or NFS or something and its _just not
working_, it could be SELinux related.

To see the current mode for SELinux, you can use `getenforce`.

To change mode, use `setenforce`.

**Remember, on boot, SELinux will be in Enforcing mode**.

Config file is at `/etc/selinux/config`. If you want to boot in Permissive mode,
for example, you'd change the config here (persistent).

So if you are troubleshooting something and you think it could be SELinux
related, try `setenforce Permissive`.
