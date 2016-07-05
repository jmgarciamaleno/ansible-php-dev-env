# Ansible PHP develop environment role

Simple Ansible role to deploy a PHP develop environment.

- Ubuntu 14.04.4
- IPtables (basic security)
- SSH server (basic security)
- Apache2 (basic security)
- PHP 5.5.9 (basic security)
- Composer

## Configuration

Edit this files to configure your project/users/groups:

- `roles/common/vars/project.yml`
- `roles/common/vars/system-groups.yml`
- `roles/common/vars/system-groups.yml`

Add the users public ssh keys to the `roles/common/public_keys/` directory. Each file name must be the same as the user.

Configured users are created in the system with ssh access through their public ssh keys and apache virtual hosts are created for everyone (user.hostname).

## Vagrant

A Vagrantfile is included to create a local VM with ip 192.168.33.101 and an 'admin' user created. The 'admin' password is requested when the machine is created:

```bash
vagrant up
```

## Usage

Once the server is up, edit the 'hosts' file (if needed) and run:

```bash
ansible-playbook -i hosts dev-env.yml
```
