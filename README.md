# Ansible PHP develop environment role

Simple Ansible role to deploy a PHP develop environment.

- Ubuntu 14.04.4
- IPtables (basic security)
- SSH server (basic security)
- Apache2 (basic security)
- PHP 5.5.9 (basic security)
- Composer

## Configuration

Configure your hosts in the ```hosts``` file and select the ones to be provisioned in the ```dev-env.yml``` file. If you just want to test this playbook check the 'Vagrant' section below.

Edit this files to configure your project/users/groups:

- ```roles/common/vars/system-groups.yml```
- ```roles/common/vars/system-users.yml```

Add the users public ssh keys to the ```roles/common/public_keys/``` directory. For the 'john.doe' user, the file must be 'john.doe.pub'.

Configured users are created in the system with ssh access through their public ssh keys and apache virtual hosts are created for every user (user.hostname).

## Vagrant

A Vagrantfile is provided to create a local VM with ip 192.168.33.101. An 'admin' user is added (password requested) when the machine is created:

```bash
vagrant up
```

## Usage

Once the server is up, edit the ```hosts``` file (if needed) and run:

```bash
ansible-playbook -i hosts dev-env.yml --ask-become-pass --ask-pass
```
