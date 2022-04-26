# CREATE SSH KEY TO REMOTE WITHOUT PASSWORD

The first, we need to create the key

    ssh-keygen -t rsa

This like

![](https://i.imgur.com/rUH6ygS.png)

In first line, we have to choose the path to save the key, second and third line we can skip this because we don't need the password to ssh server

The next, we have to config public key for SSH Server:

    nano /etc/ssh/sshd_config

Edit lines following

    PubkeyAuthentication yes
    AuthorizedKeysFile .ssh/authorized_keys

We need rename `id_rsa.pub` to `authorized_keys`

    cd /home/<user>/.ssh
>
    mv id_rsa.pub authorized_keys

After that, we come to config private key for SSH Client:

Use `sftp` to copy file `id_rsa` from server to your client. And we have to edit file config ssh for client

    nano /etc/ssh/ssh_config

Edit this lines:

    Host <IP_SERVER>
        PreferredAuthentications publickey
        IdentityFile "<PATH_PRIVATE_KEY>"

And now, we can ssh to server without password. Like this

![](https://i.imgur.com/mH21vTF.png)
