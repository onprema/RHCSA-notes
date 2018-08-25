### Reset root pw
1. Interrupt boot process, select OS, press `e`
2. Append `rd.break` to "linux16" line, press `Ctl-x`
3. `mount -o remount,rw /sysroot`
4. `chroot /sysroot`
5. `passwd`
6. `exit`
7. `touch /.autorelabel`
8. `exit`

### Bringing up a connection
1. `nmcli con mod eth0 connection.autoconnect yes`
2. `nmcli con mod eth0 ipv4.dns 8.8.8.8`

### Modify GRUB timeout
1. `vim /etc/default/grub`
2. `grub2-mkconfig -o /boot/grub2/grub.cfg`

### Configure umask
1. `vim /etc/bashrc`
2. `vim /etc/profile`

### Create a general partition
1. `fdisk`
2. `mkfs`
3. `mount`
4. edit `/etc/fstab`
5. `mount -a`

### Create a swap partition
1. `fdisk` (select "swap" type)
2. `mkswap`
3. `vim /etc/fstab` (UUID=123 swap swap default 0 0)
4. `swapon -a`

### Create a logical volume
1. `fdisk` (select "LVM" type)
2. `pvcreate /dev/PARTITION`
3. `vgcreate --size VGNAME PARTITION`
4. `lvcreate --size VGNAME -n LVNAME`
5. `mkfs.FS /dev/VGNAME/LVNAME`
6. `mkdir /mountain`
7. `mount /dev/VGNAME/LVNAME /mountain`
8. `vim /etc/fstab` (/dev/VGNAME/LVNAME /mountain FS defaults 0 0)

### SELinux httpd
1. `semanage fcontext -a -t httpd_sys_content_t '/var/web(/.*)?'`
2. `restorecon -v -R /var/web`

### Set SELinux to Permissive
1. `vim /etc/selinux/config`

### ACLs
1. `getfacl` / `setfacl -m u:user:rwx FILE`

### Cron jobs
1. `crontab -eu USER`
2. Look at `/etc/crontab` for format

### Configure NTP server
1. `vim /etc/chrony.conf`
2. `chronyc --help`

### Mounting a CIFS with samba
1. `yum install samba samba-client cifs-utils nfs-utils`

### Mounting shares in /etc/fstab
```
UUID=123 / xfs defaults 1 1
//10.0.1.250/public /mnt/sambashare cifs username=user,password=pass 0 0
10.0.1.250:/nfsshare /mnt/nfsshare nfs defaults 0 0
```
Always check `mount -a` for errors before rebooting

### Configure LDAP
?
