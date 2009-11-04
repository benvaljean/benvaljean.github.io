---
layout: post 
title: Public key authentication for SSH
---

### Check Server Config

Ensure the following settings are set in /etc/ssh/sshd\_config:

    RSAAuthentication yes
    PubkeyAuthentication yes
    AuthorizedKeysFile     %h/.ssh/authorized_keys

Many distrubutions have these settings by default, `AuthorizedKeysFile`
could have the `%h` omitted - this is OK.

### Create keys

Logon to the server you wish to connect TO, as the user you wish to
connect as:

    cd ~
    ssh-keygen -t rsa
    cat ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys
    cat ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys2
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized*

Copy the `~/.ssh/id_rsa` file to the server you are connecting FROM as
the equivalent `~/.ssh/id_rsa` file.

### Troubleshooting

Use the `-vvv` switch to allow verbose mode of ssh

#### Erroneous verbose mode error messages

The following look like errors but they are perfectly OK and even appear
when a sucessful public key authentication has taken place:

    debug3: Not a RSA1 key file /home/username/.ssh/id_rsa.
    debug2: key_type_from_name: unknown key type '-----BEGIN'
    debug3: key_read: missing keytype
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug3: key_read: missing whitespace
    debug2: key_type_from_name: unknown key type '-----END'

This is perfectly normal as we are using RSA2 keys!

    debug1: Unspecified GSS failure.  Minor code may provide more information
    No credentials cache found

The above error can relate to outdated SSH keys, particularly on Debian
systems, although it also occurs when authentication has completed OK.

#### Log file locations

Debian/Ubuntu: `/var/log/auth.log`\
Redhat/CentOS: `/var/log/secure`

#### Check Ownership and modes

From /var/log/secure:

    Authentication refused: bad ownership or modes for file /home/username/.ssh/authorized_keys2

Check that your authorized\_keys file is owned by the user you are
logging on as and has 600 permissions.

[Category:Linux](Category:Linux "wikilink")
