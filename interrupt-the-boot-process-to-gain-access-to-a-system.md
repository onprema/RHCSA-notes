## Interrupt the Boot Process to Gain Access to a System
For example, resetting your root password.

Must be in front of physical machine or virtualized machine because we need the
grub boot menu.

1. `reboot`
2. press any key
3. select the kernel you want to boot into
4. press `e` to edit config
5. search for the line that starts with linux16...
6. append `rd.break` at the end of the line -> this enters you in initramfs debug shell
7. press C-x to resume boot process, you will be brought to a prompt
8. `mount -oremount,rw /sysroot` -> gives rw perm on /sysroot
9. `chroot /sysroot` -> now /sysroot is acting as /
10. `passwd` to change the root password
11. touch /.autorelabel -> required for selinux to successfully change root pw
12. `exit` leaves initramfs shell and reboots the system
