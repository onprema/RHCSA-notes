## Boot Systems into Different Targets Manually
- Targets are dependency groupings
- `systemctl list-units --type=target` lists all targets on the system
- the .service files in /usr/lib/systemd/system are SERVICES. They are configuration files that represent services. They have replaced bash scripts. They are what systemd reads to run services.
- After: lists units that need to be started before the service can run.
- WantedBy: when a service is `enable`d by systemd, it will be added to whatever follows WantedBy=
- WantedBy=multi-user.target -- when the system moved into the multi-user target, THEN the configuration file will be opened/executed.
- `systemctl list-dependencies multi-user.target` lists the dependency tree of the multi-user target
- multi-user.target: multiple users can be logged in -- text-based interface
- graphical.target: GUI
- emergency.target: boots us into a root command prompt and mounts a read-only FS
- rescue.target: used for troubleshooting
```
graphical.target
|-> multi-user.target

whenever graphical.target is called, it will call multi-user.target, too.
```
- `systemctl isolate NAME` switches to NAME.target, but only if AllowIsolate=yes is set in the target's config.
- `systemctl isolate graphical.target` will start everything required to run the graphical interface
- `systemctl get-default` shows default target
- `systemctl set-default NAME` sets the default target to NAME.target
- `/etc/systemd/system` additional configuration files that will overwrite anything with the same name in /usr/lib/systemd/system


**Manually changing the target that starts on boot.**
1. `reboot`
2. press any key to interrupt boot sequence
3. edit the linux version you want to edit
4. find line that starts with linux16... (invoking the kernel)
5. append systemd.unit=NAME.target at the end of that line
6. press C-x to continue booting
... Now the system will boot in whatever target you specified in step 5

For example, you could go from graphical.target to multi-user.target if you
wanted to have a non-GUI experience. Or multi-user.target to rescue.target for
troubleshooting.
