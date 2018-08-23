## Restore Default File Contexts

`/.autorelabel` will relabel all files based on the proper context.

What determines that context is shown in `semanage fcontext -l`.

Example:
- Edit `/etc/httpd/conf/httpd.conf` and change the DocumentRoot to `/content`
- Also change the `<Directory>` block to `/content`
- `systemctl reload httpd` to server from `/content`
- `chown -R apache:apache /content`
- `echo "hello world" > /content/index.html`

Now if you go to mysite.com/index.html you'll get a 403 **because index.html
doesn't have the appropriate context type**.

To change the context: `semanage fcontext -a -t httpd_sys_content_t '/content(/.*)?'`

Then do `restorecon -R -v /content` to make those changes effective.

Summary - How to add/change a context:
1. create an entry with `semanage fcontext`
2. use `restorecon` on the file/dir

Note: `semanage fcontext -d "/content(/.*)?"` to **d**elete an entry.
