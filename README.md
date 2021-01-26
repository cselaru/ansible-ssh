# ansible-ssh

Ansible installation has all necessary parameters for connecting to managed hosts. Duplicationg this parameters in `~/.ssh/config` is not convenient, especially if dynamic inventory is used.

This script parses ansible configuration to get that parameters. Just place it somewhere in your `$PATH`, like `~/.local/bin`. 

Considered inventory variables: `ansible_host`

How it works:

```console
user@work$ cd my_ansible_repo
user@work$ cat hosts | grep server1
server1 ansible_host=192.168.0.1 ansible_user=root ansible_port=2222
user@work$ cat ansible.cfg | grep ssh_args
ssh_args = -C -o ControlMaster=auto -o ControlPersist=60s

user@work$ ansible-ssh server1
ssh_args:  -C -o ControlMaster=auto -o ControlPersist=60s
ansible_host: 192.168.0.1
ansible_user: root
ansible_port: 2222
ansible_ssh_common_args:
result command: ssh ubuntu@192.168.0.1 -C -o ControlMaster=auto -o ControlPersist=60s -p 2222

root@server1#
```

Options:

* `[-i INVENTORY]` specify inventory file for ansible

* all options and arguments after the hostname are passed to ssh.

# Requirements

* Ansible
* [jq](https://stedolan.github.io/jq/)
* set the ANS_USR env variable to the desired user you want to use to login to your hosts
* set the ANS_JUMP_HOST env variable to the desired jumphost hostname

**P.S.** If you like it, don't forget to put a star on its [github repo](https://github.com/selivan/ansible-ssh).
