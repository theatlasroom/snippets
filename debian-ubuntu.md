# Debian / Ubuntu
## Add new user + grant sudo
```
# as root
# create user
sudo adduser <username>
# grant sudo privileges
visudo

# add this line
# User privilege specification
<username>  ALL=(ALL:ALL) ALL
```

## Copy ssh key onto new machine
```
$ ssh-copy-id -i ~/.ssh/<ssh-key>.pub <user>@<server>
# OR
$ cat ~/.ssh/<ssh-key>.pub | ssh <user>@<server> "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"
```
