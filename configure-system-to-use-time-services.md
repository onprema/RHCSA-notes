## Configure a System to Use Time Services

`timedatectl` provides information about the system's configured time.

If you don't know your timezone you can use `tzselect`.

`chronyd` is the default daemon that NTP (network time protocol) uses in RHEL7.
It was created to help keep time services synced.

`chronyc` is the CLI for `chronyd`.

If you make changes to you time settings (via `timedatectl`) you need to let
`chronyd` know about the changes by restarting the `chronyd` service.

Network Time Protocol (NTP) communicates with multiple servers and attempts to
synchronize the system's time to what the server's consider the correct time.

`/etc/chrony.conf` is the config file for `chronyd`.
