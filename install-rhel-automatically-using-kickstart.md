## Install Red Hat Enterprise Linux Automatically Using Kickstart

What is Kickstart?
`/root/anaconda-ks.cfg` is the configuration file for the Kickstart script.

When you install RHEL7 you go through an options screen (wizard).
You select what hard drive it should be installed on
You add a password for the root user
You add another user
etc.

In a large organization you might have thousands of RHEL7 servers. Manual
installation could take ages. So how about you make a script? That's what
Kickstart is about.

The script answers all those questions during installation, like root password,
what hard drive, preferences, language, network, time zone, etc.

You can also pre-install packages like `httpd`, `vim`, etc.

How do you set this up without writing an entire Kickstart script from scratch?
- You can look at `/root/anaconda-ks.cfg` as a template.
- You can `yum install system-config-kickstart` to get a GUI interface to create
  a Kickstart file.

Run `system-config-kickstart` to launch the wizard. This is nice.

How do I find documentation for Kickstart?
`rpm -qd pykickstart` (**d** for documentation)

In order for Kickstart to work it needs to connect with a PXE server, usually a
virtual machine. **PXE** = pre-boot execution environment. The PXE server reads
the `.ks` config file and attempts to install the OS.
