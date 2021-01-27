# ansible-ssh

Ansible installation has all necessary parameters for connecting to managed hosts. Duplicationg this parameters in `~/.ssh/config` is not convenient, especially if dynamic inventory is used.

This script parses ansible configuration to get that parameters. Just place it somewhere in your `$PATH`, like `~/.local/bin`. 

The script was modified so that it supports this scenario: you have to use a jumphost/bastion and the username is different then the one used by Ansible (NPA account).

How it works:

```console
user@work$ cd my_ansible_repo
user@work$ cat hosts | grep server1
server1 ansible_host=192.168.0.1 ansible_user=root ansible_port=2222

user@work$ ansible-ssh server1
ansible_host: 192.168.0.1
result command: ssh someuser@192.168.0.1

root@server1#
```

Options:

* `[-i INVENTORY]` specify inventory file for ansible

* all options and arguments after the hostname are passed to ssh.

# Requirements

* Ansible
* [jq](https://stedolan.github.io/jq/)
* set the correct values in ansible-ssh.config and put the file in your home folder

**P.S.** The original code can be found here, please give them some kudos, as i just improved it a bit for my scenario [github repo](https://github.com/selivan/ansible-ssh).
