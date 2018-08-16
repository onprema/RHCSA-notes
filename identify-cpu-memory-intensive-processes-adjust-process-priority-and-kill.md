## Identify CPU/Memory Intensive Processes, Adjust Process Priority and Kill Processes
- `pgrep`
- `pkill`
- default `kill` is SIGTERM (15) and its "nice". It allows the process to finish before it is terminated.
- `kill -SIGKILL` (9) is immediate
- SIGHUP, hangup, is used to configure/reload the controlling process of a terminal. Its what happens when you click the X in the upper corner of a window.
- SIGINT == C-c
- SIGSTOP cannot be ignored
- SIGTSTP can be ignored
- !! start using `w` !!
- `jobs` shows what background processes are running
- `ps axo pid,comm,nice` -> cool way to format the ps display
- "Nice Level" - the niceness of a process
- niceness means the priority to CPU utilization
- LOWER niceness = higher priority
- `ps -u` -> linux/POSIX syntax
- `ps u`  -> BSD syntax
- both have different behavior
- If you are running a web server, like httpd, you might want to set the niceness level of the httpd processes to have a higher priority in order to optimize!
- niceness level ranges from -20 to 19
- it's like priority mail
- only priveleged users can increase priority, but anyone can decrease it.
- `nice -n -10 httpd` will start `httpd` with a niceness level of -10
- `renice -n 0 $(pgrep httpd)` will change the niceness level of all httpd
  processes to 0
`load average: 0.03, 0.07, 0.05`
- cpu load for the past 1min, 5mins, 15mins - this can be skeweded depending on
  how many processes are running on the system.
- true load is more like `load / # of processors`
- top toggle keys: `t` (tasks), `m` (memory), `l` (uptime), `b` (bold), `r`
  (renice), `k` (kill)
