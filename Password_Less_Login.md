
Link: https://debian-administration.org/article/152/Password-less_logins_with_OpenSSH

# Password less logins with OpenSSH

- generate a new keypair

$ ssh-keygen -t rsa

~/.ssh/id_rsa and ~/.ssh/id_rsa.pub

- copy public key to remote machine

ssh-copy-id -i ~/.ssh/id_rsa.pub username@myremotehost

This will prompt you for the login password for the host, then copy the keyfile for you, creating the correct directory and fixing the permissions as necessary.

The contents of the keyfile will be appended to the file ~/.ssh/authorized_keys2 for RSA keys, and ~/.ssh/authorised_keys for the older DSA key types.

- test connect to remote machine

$ ssh myremotehost uptime
09:52:50 up 96 days, 13:45,  0 users,  load average: 0.00, 0.00, 0.00

- What if it doesn't work?

1. If the remote server doesn't allow public key based logins

Edit /etc/sshd/sshd_config:
    RSAAuthentication yes
    PubkeyAuthentication yes

/etc/init.d/ssh restart

2. File permissions cause problems

access to remote machine
cd
chmod 700 .ssh

3. Your keytype isn't supported

If you're logging into an older system which has an older version of OpenSSH installed upon it which you cannot immediately upgrade you might discover that RSA files are not supported.

Add public key to ~/.ssh/authorized_keys
