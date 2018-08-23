## Configure Firewall Settings Using firewall-config, firewall-cmd, or iptables

`netfilter`

`iptables` / `ip6tables`

`firewalld` is a lot easier to use than iptables.

`yum install firewalld firewall-config`
`systemctl start firewalld && systemctl enable firewalld`

**Know the differences between a runtime change and a persistent change. Know
_when_ and _why_ you need to do either one.**

`firewall-cmd` is the CLI tool for firewalld.

`firewalld` groups all of your rules inside of a **zone**.

A zone can have specific allowed IP addresses.

`firewall-cmd --get-default-zone` shows your default zone. Whenever you add a
rule, unless you specify the zone, it will be set on the default zone.

Specify the zone with `--zone=ZONE`.

**`firewall-cmd` support double-tab completion!**

If you do `firewall-cmd --reload` the runtime changes will be wiped!

Fortunately, it's really easy to make changes persistent, you just need to add
`--permanent`. **But you need to do `--reload` again for those changes to
apply** (or reboot).

Zones are basically just groups of IP addresses, which make it easier to group
machines together and apply rules for groups instead of individuals.

Example: running an Apache server, but the website won't load because the
firewall isn't allowing traffic through port 80.
- `firewall-cmd --zone=public --add-port=80/tcp` will open up port 80
- But remember that if you `--reload` or reboot, that port will close
- You could also do `--add-service=http`.

`firewall-config` is the GUI tool for `firewalld`.

**Panic mode** (`--panic-on`) will shut down all ports, rendering the system
unusable.
