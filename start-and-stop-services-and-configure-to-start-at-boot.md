## Start and Stop Services and Configure Services to Start Automatically at Boot

Services are controlled with `systemd`, which utilizes _targets_. When our
system moves into a specific target, all associated services (and their
dependencies) will be started.

To see what services are enabled/disabled you can list the unit configuration
files via `systemctl list-unit-files --type=service`.

When we enable our service, how do we know what target it belongs to?
`systemctl get-default` shows the current target the system is in.
`systemctl list-dependencies multi-user.target` lists the dependencies for the
multi-user target.

If we do `systemctl enable httpd` it will add the httpd.service as a dependency
of the multi-user.target (or graphical.target if you're in a gui). `httpd` will
start on boot **even if it wasn't running previously**.

The `multi-user.target` is a dependency of the `graphical.target`. In other
words **graphical.target _depends on_ multi-user.target**.
