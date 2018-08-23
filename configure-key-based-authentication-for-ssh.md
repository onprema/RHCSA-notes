## Configure Key-Based Authentication for SSH

Key-based authentication allows us to generate a private key and an associated
public key. The _public_ key will be stored on the remote machine we are trying to
connect to. The _private_ key will be stored on our machine (the host).

Private keys should always be protected.

The public key is used to _verify the private key_.

`ssh-keygen` is the tool to generate the key pairs. The default on RHEL7 is of
type rsa, but you can specify with `-t`.

A **passphrase** is a good thing to assign because if someone happens to get
your private key, they will need to crack the passphrase, too.

`ssh-copy-id` is a script that logs into a remote machine that is running ssh,
and copies _that_ machine's public key into `/.ssh/authorized_keys` on the host.
This then allows these two machine to connect with eachother via ssh.

If you set a passphrase and you are tired of entering it each time you connect
with a client, you can do this:
- `ssh-agent bash` starts a fresh ssh-agent bash session.
- `ssh-add` adds the passphrase in a cache for the current bash session.
- Now you don't have to enter the passphrase every time.

Passwordless authentication.
