## Use Boolean Settings to Modify System SELinux Settings

Booleans allow runtime modification of security policy without having to load a
new policy.

For example, the boolean httpd_enable_cgi allows the httpd daemon to run cgi
scripts. If the administrator does not want to allow execution of cgi scripts, 
he can simply disable this boolean value. if it is enabled.

`getsebool -a` lists all SELinux boolean values

`semanage boolean -l` also lists (nice, more verbose!)

`setsebool` is used to set a boolean `on` or `off` (support tab-completion!) --
**This is not persistent**. To verify do `semanage boolean -l` and see it's
_default_ value.

Well, how do you make is persistent?

`setsebool -P` - **P** for Persistent.
