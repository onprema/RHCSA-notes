## Schedule Tasks Using at and cron

`at` allows us to schedule the execution of a command at a later point in time.

Examples:
`at now +5 minutes` execute 5 minutes from now
`at now +5 hours` execute 5 hours from now

You will be brought to a prompt (`at> `) where you can enter commands. When you
are done, enter C-d (EOF).

`atq` lists the job queue.
`atrm 1` removes job #1.

`/etc/at.deny` is like .gitignore, except you enter username(s) that you want to
deny use of the `at` utility.

`/etc/at.allow` is the inverse. Only users who are listed inside this file can
use `at`.

`cron` also has these .allow and .deny files.

`crontab` maintains crontab files for _individual users_.
`cron` maintains crontab files for the system.

**`/etc/crontab` displays a nice breakdown of the format of a cron job definition!**

Note: the computer must be turned on in order for cron to execute it's tasks.
`anacron` allows you to bypass this limitation. You can edit the config in
`/etc/anacrontab` to add a "more persistent" cron job.

`anacron -n` will run all the jobs in `/etc/anacrontab` immediately, ignoring
any delays.

`anacron` knows when the last time it's entries have been executed by the
timestamps found in the `/var/spool/anacron/` directory.

`5 0 * * fri root /root/myscript.sh` runs every Friday at 12:05

In `/etc/` there are `cron.daily/`, `cron.weekly/`, `cron.hourly/`, etc. You can
put scripts in these directories and they will execute appropriately (daily,
weekly, hourly, etc).

(If you look in `/etc/anacrontab` you will see these directories).

But what if you want to execute a script every x minutes?

You'd make a custom cron and put it in `/etc/cron.d/`.

For example, `*/1 * * * * root wall hello` will execute the `wall` command every
minute, which is like an alert across the system that says "hello".

The above line can live in a file (you can name it whatever you want). As long
as its in `/etc/cron.d/` it will get picked up by the cron daemon.

**BONUS: `rpm -qc PACKAGE` queries for configuration files of a given package**
For example, `rpm -qc httpd` will list all config files that were installed with
the `httpd` package.
