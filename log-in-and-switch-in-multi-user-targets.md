## Log in and Switch Users in Multiuser Targets
- a 'target' is a group of config files, or services, that start when the system
navigates into said target. multi-user.target allows us to have multiple users
on the system.
- interactive shell - a shell that a user types stuff in to log-in shell
- ~/.bash_profile is a script that runs when a user enters a log-in shell
- when you first log in to a system you are in a log-in shell.
- then, if you do `su user2` you enter an interactive shell.
- ~/.bashrc is executed when you enter into an interactive shell.
- ~/.bash_profile is NOT executed in an interactive shell. Only log-in shell.
- `su -`
- `su -l`
- `su --login`
- These all represent log-in shell
- if you want to log in with the customizations (env) of the current user, do `su`
- if you want to log in and load everything in .bash_profile, do `su -`
- `/etc/profile` is loaded when *any* user logs in to the system
- every user will have a /home/<user>/.bash_profile where you can customize
