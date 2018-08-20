## Configure Networking and Hostname Resolution Statically or Dynamically: Hostname Configuration

`dhcp` is responsible for automatically assigning IP addresses to network
interfaces. It can also be set manually using `nmcli` (static IP addressing).

`/etc/resolv.conf` holds configuration for which DNS name servers the system
will query when it attempts to resolve a domain name.

The `search` directive in this file sets a base domain for resolution of domains
with subdomains. For example if you have `search mydomain.com` and you attempt
to resolve `lee.mydomain.com` you would only need to query for `lee`. You could
do `ssh lee` instead of `ssh lee.mydomain.com`.

"Poisoning DNS" is to edit `/etc/hosts` to supply your own domain resolution.

`/etc/nsswitch.conf` holds configuration for many things, including the DNS
resolution steps. You can set it to look at files (`/etc/hosts`) before dns
(defined in `/etc/resolv.conf`), or even specify a dns server my domain.

You can use `hostnamectl` to change the system's host name (which can be found
in `/etc/hostname`). Note: you'll need to do `exec bash` to see the changes on
your prompt.

You can change the DNS nameservers using `nmcli con mod eth0 ipv4.dns 8.8.8.8`,
for example. This change will not show up in `/etc/resolv.conf` until you take
down then bring up the connection again, or reboot. But it **is** persistent.

`getent hosts google.com` will show the IP addresses linked to google.com. Good
way to test DNS poisoning.
