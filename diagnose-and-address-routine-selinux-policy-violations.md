## Diagnose and Address Routine SELinux Policy Violations

How do you know what booleans you need to address when you're troubleshooting?

`yum install setroubleshoot-server`

This will install a command called `sealert` (the CLI tool for
`setroubleshoot-server`).

SELinux creates logs at `/var/log/audit/` -- it's not very human-friendly to
read. But we can use `sealert -a` to scan these log files.
