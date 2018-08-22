## Change Passwords and Adjust Password Aging for Local User Accounts

`/etc/login.defs` allows us to adjust default password aging controls.

But how do we change it for individual users?

Our three tools:
- `passwd`
- `usermod`
- `chage`

`chage` manages password policy.

When we use these tools we modify `/etc/passwd` and/or `/etc/shadow`.

`/etc/shadow` should have 000 permissions. Only root should be able to see it.

Let's say we have a user that needs an account to the system, but they don't
need an interactive shell. You can do `usermod -s /sbin/nologin USER`.

`chage -l USER` basically shows what is in the `/etc/shadow` file for `USER`,
but in a human-friendly way.

`chage -E 2018-09-06 USER` expires the _account_ on 2018-09-06.

_Password_ expiration refers to the number of days the password must be changed.
_Account_ expiration basically kills your account. If your account is expired
you'll get denied access to the system.

`chage -E -1 USER` reactivates USER's account (if it was expired)

`chage -d 0 USER` **sets the last password change date to 0, effectively making
the user enter a new password next time they log in**.

"Password Inactive" = the number of days after a password expires until the
account is locked.

`chage -I 5 USER` makes it so that if USER doesn't log in for 5 days after the
password expires, it wil automatically lock the account and they will have to
contact the admin to get access to their account.
