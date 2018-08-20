## Configure a Physical Machine to Host Virtual Guests

Objective: configure a system to start a virtual machine on boot.

`libvirtd` is the "Virtual Machine Manager" GUI app. This must be enabled.

Virtual Machine Manager is kind of like VirtualBox. You can create a VM inside
RHEL7. It's faster than VirtualBox and it utilizes resources better than
VirtualBox, apparently.

Sometimes you don't have networking set up in your VM so you need to bring it up
manually. You can bring one up via `nmcli con up DEVICE`. You can see what
devices (NICs) are available on the system at `/sys/class/net`.

How can I configure the connection to be up at boot-time?
`nmcli con mod "NAME" connection.autoconnect yes` (if you forget, you can always
double-tab to see the syntax).

Note: virtual machines are also called "domains" sometimes.

How can I get the VM to start on boot?
- `libvirtd` must be enabled!
- Use `virsh` to enter the CLI version of Virtual Machine Manager.
- Within virsh, do `autostart NAME`
- That's all!

So what we are doing here is:
- Installing KVM (Virtual Machine Manager) on RHEL7
- Bringing up a connection, so it can communicate with the world (via the host's
  network).
- Configuring the VM to start automatically whenever the physical machine boots.
