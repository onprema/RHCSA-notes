## Locate and Interpret System Log Files and Journals
- systemd comes with journald (man systemd-journald)
- we can use journald (`journalctl`) to view log info
- journald is not persistent, by default. if you reboot, the contents of
  journald will be destroyed. this can be changed in `/etc/systemd/journald.conf`
- anything in `/run` is not persistent
- any event like writing to a log file is able to be viewed through `journalctl`
- don't overthink it. journalctl makes notes of any messages coming into the
  system through systemd.
- `journalctl -x` provides additional explanantion text, if available
- `rsyslog` is a logging service to create generic log files
- `/etc/rsyslog.conf` has rules that define what log messages go where
- `systemd-analyze` shows how fast the system booted up
- `systemd-analyze blame` shows which service took how much time
