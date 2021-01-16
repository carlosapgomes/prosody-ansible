# Prosody Ansible

This is an ansible playbook to setup a Debian server running Prosody XMPP.

## Login as `root`

`ssh root@your.server.ip.address`

## Change root password

`passwd`

## Install sudo

As root:

`apt update && apt upgrade && apt install sudo`

P.S.: consider restarting the system before proceding.

## Create a new user named, for example, "john"

`adduser john`

## Grant administrative privileges to the new user

As root:

`usermod -aG sudo john`

## Allow the new user to use sudo without a password

As root:

`visudo`

Add the following lines:

```
# Allow members of 'john' group to sudo without password

%john ALL=(ALL) NOPASSWD: ALL
```

## Create SSH keys locally

`ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "john@example.com"`

## Copy the public key to the remote server

`ssh-copy-id -i ~/.ssh/id_ed25519 john@your.server.ip.address`

If you have many keys in your `~/.ssh` folder, you may get an error like:

`Received disconnect from xxx.xx.xx.xx port xx: Too many authentication failures`.

In that case, try this:

`ssh-copy-id -o PubkeyAuthentication=no -i ~/.ssh/id_ed25519 john@your.server.ip.address`

## Login using your public key

`ssh -i ~/.ssh/id_ed25519 john@your.server.ip.address`

## Set DNS Records in your Domain Name Registrar

`A Record @ xx.xx.xx.xx`

`A Record chat xx.xx.xx.xx`

`SRV Record _xmpp-client _tcp 0 5 5222 chat.domain.name`

`SRV Record _xmpp-server _tcp 0 5 5269 chat.domain.name`

`TXT Record _xmppconnect _xmpp-client-xbosh=http://chat.domain.name:5280/http-bind`

## Resources:

[DNS Config](https://youtu.be/-0M0NeZ_cU4)

[How to Set Up Prosody XMPP Server on Ubuntu 20.04](https://www.linuxbabe.com/ubuntu/install-configure-prosody-xmpp-server-ubuntu-20-04)

[dank-selfhosted](https://github.com/cullum/dank-selfhosted)

[Prosody Server Setup 0.10](https://www.cyberpunk.rs/prosody-server-setup-0-10-xmpp)

[Archlinux Prosody](https://wiki.archlinux.org/index.php/Prosody)

[The Practical Administrator](https://practical-admin.com/blog/private-chat-using-prosody/)

[30-minute Practical Linux Project: XMPP Chat Server Setup, Start to Finish](https://www.youtube.com/watch?v=-0M0NeZ_cU4)
