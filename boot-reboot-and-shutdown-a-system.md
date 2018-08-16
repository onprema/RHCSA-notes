# Boot, Reboot and Shutdown a System
- `reboot` shuts down the OS, goes through Grub initialization process, ramfs, restarts services, then hands control over to systemd. `systemctl reboot` is the same.
- `shutdown -r +5 System will reboot` invokes the `wall` command to announce to
all the users on the system that there will be a reboot in 5 minutes.
- `shutdown -c` cancels reboot and lets users know it was cancelled cancels reboot and lets users know it was cancelled.
- `shutdown -r 00:00` will shutdown at midnight
- `init 0` will shutdown the system. it's being depricated but still used for
backwards-compatibility
- "targets" have replaces "run levels"
- a target is what our system navigates in an out of to shutdown a system targets are at /usr/lib/systemd/system
