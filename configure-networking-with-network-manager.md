## Configure Networking and Hostname Resolution Statically or Dynamically: Network Manager

`ls /sys/class/net` lists network interfaces

`nmcli` is the NetworkManager CLI tool
`nmcli dev status` checks status of network interfaces

`nm-connection-editor` and `nmtui` are utilities to configure network
connections. You can just type `nm` and double-tab to see a list of `nm`
utilities! So if you forget the syntax **use double-tab**.

Think of a connection as a _configuration_ that is attached to a device.
Connection configs are located in `/etc/sysconfig/network-scripts`.

To bring up a new connection do `nmcli connection add con-name "myconnection"
autoconnect yes type ethernet ifname eth1` that's it! :P. (**use nmcli
double-tab**).

To bring down a connection do `nmcli connection down "myconnection"`.

It appears that you can only have one active connection per interface (?).
