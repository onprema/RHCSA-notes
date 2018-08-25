# LA Practice Exam Questions

You're given a VM that has a RHEL7 image.

### Start the Guest VM
- `yum groupinstall "Virtualization Platform"`
- `yum groupinstall "Virtualization Client"`
- `systemctl start libvirtd`
- `systemctl enable libvirtd`
- **Note: on LA for some reason you only need to do `yum install virt-manager`,
  if you install these other packages it won't work**.
- `virt-manager` (start VM and open console)
- You should be brough to login prompt for `root`
- Reset the VM because you won't have the password.
- Interrupt boot process. Navigate to OS. Press `e`
- Find "linux16" line and append `rd.break`
- Ctl-x to resume boot
- `mount -o remount,rw /sysroot`
- `chroot /sysroot`
- `passwd`
- `exit` (exit chroot jail)
- `touch /.autorelabel`
- `exit` (resume boot, should get prompted for root login)

Once you're in the RHEL7 VM do `yum install bash-completion`

**There might not be any enable repos**!

### Create a new repo
- Look at `/etc/yum.repos.d/*.repo` _on the host_ for help with the syntax.
- `vi /etc/yum.repos.d/myrepo.repo`
```
[myrepo]
name=My Repo
baseurl=http://mirror.whatever.com/they-should-give-you-this/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-RHEL-7
```

**There might be a network issue**!

### Bring up a connection
- `ip addr show` will display interfaces, if eth0 doesn't have an ip address
  then we have problems
- `nmcli con mod eth0 connection.autoconnect yes`
- `nmcli con up eth0`
- `nmcli con mod eth0 ipv4.dns 192.168.122.1` or whatever the host's address is
- `ip addr show` to verify

Now you should be able to install packages, like `bash-completion`. Since there
is a network connection, now you can leave the KVM console and `ssh` into the
guest VM!

--------------------------------------------
> Do any tasks related to GRUB, LVM or partitions first! These are the things
> that could cause major problems (ie: not being able to boot).
--------------------------------------------

### Modify the GRUB timeout from 5 seconds to 1 second
- `vim /etc/default/grub`
- change `GRUB_TIMEOUT=1`
- `grub2-mkconfig -o /boot/grub2/grub.cfg`
- `reboot`
- Watch the machine boot up via KVM. There should only be a 1 second delay at
  the menu screen where you can choose your OS.

--------------------------------------------
> You will want to reboot after any exercise that could affect the boot process!
--------------------------------------------

### Create an 800M swap partition on the vdb disk and ensure it is persistent. Use the UUID to enable persistence. 
- `lsblk` to look at disks
- Before you move on you should read the other instructions and make sure you
  don't make a partition that it too small or something like that.
- `fdisk /dev/vdb`
    - `n` new partition
    - `p` primary
    - `1` default (partition #1)
    - `first sector` default
    - `last sector` +800M
    - `t` set type to swap
    - `w` write and exit
    - `partprobe`
- `lsblk` to verify vdb1 exists
- `mkswap /dev/vbd1`
- `blkid` to verify the swap partition was created ans view its UUID.
- `vim /etc/fstab`
    - Add `UUID=123123123123123 swap swap defaults 0 0`
- `swapon -a`
- `cat /proc/swaps` to verify that swap space is ready.
- `reboot`
- `cat /proc/swaps` again

### Create a new logical volume, LV-A, with a size of 30 extents belonging to the volume group, VG-A, with a PE size of 32M.
- `lsblk` to see your blocks
- `fdisk /dev/vdb`
    - `n` new partition
    - `p` primary
    - `default` first and last sector
    - `t` choose LVM
    - `w` write and quit
- `partprobe`
- `yum install lvm2` (you can do `yum whatprovides pvcreate` if you don't know
  what package you need to install)
- `pvcreate /dev/vbd2`
- `vgcreate --physicalextentsize 32M VG-A /dev/vdb2`
- `lvcreate -l 30 VG-A -n LV-A`
- `lvdisplay` to check your work
- `mkfs.ext4 /dev/VG-A/LV-A`
- `mkdir /data`
- `mount /dev/VG-A/LV-A /data`
- `vim /etc/fstab`
    - Add `/dev/VG-A/LV-A  /data  ext4  defaults  0  1`
- `mount -a` to make sure there are no errors in `/etc/fstab`
- `lsblk` to verify
- `reboot`
- `lsblk` to verify, again.


### Create a new logical volume, LV-A, with a size of 30 extents belonging to the volume group, VG-A, with a PE size of 32M. 
- `yum install httpd`
- `mkdir /var/web`
- `chown -R apache:apache /var/web`
- `echo "hello" > /var/web/index.html`
- `vim /etc/httpd/conf/httpd.conf`
    - Change `DocumentRoot` to `/var/web` in three places.
- `systemctl restart httpd`
- `systemctl enable httpd`
- If things don't work...
    - `semanage fcontext -a -e /var/www/ /var/web` Sets the context of `/var/web` to `/var/www`
    - `restorecon -Rv /var/web` Makes everything consistent
    - `firewall-cmd --permanent --add-service=http && firewall-cmd --reload`


### Set SELinux to be in Permissive mode
- `vim /etc/selinux/config`
- Change `SELINUX=permissive`
- `sestatus`
- `shutdown -r now`
- `sestatus` to verify it's permissive


### Configure Umask to ensure all files created by any user cannot be accessed by "other" users
- `umask` to see current mask
- `vim /etc/bashrc`
    - change `umask 007` for regular users
    - change `umask 027` for priveleged users
- do the same in `/etc/profile`
- log out, then log back in and check `umask` again.
- `touch file1` and check permissions


### Make a directory for the Instructors group and ensure that all files in that directory are owned by the group Instructors
- `mkdir /instructors`
- `chown :Instructors /instructors`
- `chmod g+s /instructors`
- Verify `cd /instructors && touch file && ll / | grep instructors`


### Access Control Lists
- `setfacl -m u:kenny:rwx /tmp/instructor_doc`
- `setfacl -m u:tom:- /tmp/instructor_doc`
- `setfacl -m g:instructors:rw /tmp/instructor_doc`
- `getfacl /tmp/instructor_doc`


### Find files in /etc/ (not deeper) that was modifified older than 720 days ago
- `find /etc -maxdepth 1 -type f -mtime +720`


### Find all log messages containing "ACPI" in /var/log/messages and export them to a file called "logs" stored in the root home directory. Then, gzip /var/log and save to /tmp/log_archive.tgz
- `grep "ACPI" /var/log/messages > logs`
- `tar -czvf /tmp/log_archive.tgz /var/log`
- `tar -xvf /tmp/log_archive.tfz` to verify


### Create a cronjob for derek that runs echo /etc/redhat-release daily at 4:27pm and redirects the output to /home/derek/release
- `su derek`
- `echo /etc/redhat-release` make sure you can do this as `derek` to the
  permissions don't screw up the cron job. **Then go back to `root`**
- `crontab -eu derek`
    - `27 16 * * * echo /etc/redhat-release > /home/derek/release`
    - `1 * * * * echo /etc/redhat-release > /home/derek/release` to test


### Configure time.nist.gov as the only NTP server
- `vim /etc/chrony.conf`
- Replace the defaults servers with `server time.nist.gov iburst`
- `systemctl restart chronyd`
- `chronyc sources -v`


### On the *host*, not the guest VM, Utilize ldap.linuxacademy.com for SSO and configure autofs to mount users' home directories on login. Ensure you utilize Kerberos
- `yum install authconfig-gtk nss-pam-ldapd pam_krb5` -> **memorize these**
- `authconfig-gtk` launches the GUI
    - User Account Database: **LDAP**
    - LDAP Search Base DN: **dc=linuxacademy,dc=com**
    - LDAP Server: **ldap://ldap.linuxacademy.com/**
    - Use TLS
    - Download Certificate - **http://ldap.linuxacademy.com/pub/cert.pem**
    - Authentication Method: **Kerberos password**
    - Check **Use DNS to locate KDCs for realms**
    - Advanced Options > **Create home directories on the first login**
- `yum install autofs nfs-utils openldap-clients` -> **memorize these**
- `vim /etc/auto.master.d/ldap.autofs`
    - Add `/home/guests /etc/auto.ldap` to mount dirs to /home/guests
- `vim /etc/auto.ldap`
    - Add `* -rw ldap.linuxacademy.com:/home/guests/&`
- `vim /etc/pam.d/sshd`
    - Add `auth    sufficient    pam_permit.so` at the top
    - Add `auth    sufficient    pam_ldap.so` at the top
- `systemctl start autofs && systemctl enable autofs`
- `systemctl restart sshd`
- `su - ldapuser1` (ldapuser1 is provided)
    - You should be brought to `ldapuser1`'s prompt and home dir
- `ls /home/guests` to verify, try writing a file
