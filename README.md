# Ansible PHP develop environment role

Simple Ansible role to deploy a PHP develop environment on Ubuntu Server 14.04.

- IPtables (basic security)
- SSH server (basic security)
- Apache2 (basic security)
- PHP 5.5.9 (basic security)
- Composer
- MySQL client

Configured users are created in the system with SSH access through their public SSH keys.

Apache virtual hosts are created for every user (user.hostname).

Apache *mod\_security* is installed but disabled by default due to often being too restrictive for a develop environment, even with base rules only activated.  
To enable *mod\_security*, edit the ```roles/common/tasks/apache-harden.yml``` file and replace ```SecRuleEngine Off``` with ```SecRuleEngine On```.

## Usage

1. Edit the ```hosts``` file and fill it with your hosts data.

2. Add the hosts to provision to the ```- hosts:``` line in ```php-dev-env.yml```.  
   The given hosts may be a single host, a group or a list of comma-separated hosts/groups.
   E.g:
     - ```- hosts: [project1-group]```
     - ```- hosts: project1-dev```

3. Add your users and groups to the files:
     - ```roles/common/vars/system-groups.yml```
     - ```roles/common/vars/system-users.yml```

4. Add the users public SSH keys to ```roles/common/public_keys/``` with format ```<USER>.pub```.  
   ```<USER>``` must coincide with the login name of the user (e.g: john.doe.pub).

5. Run: ```ansible-playbook -i hosts php-dev-env.yml --ask-become-pass --ask-pass```

## Vagrant

A Vagrantfile is provided to create a local VM with ip ```192.168.33.101``` and test this playbook against it.  
An ```admin``` user is added (password requested) when the machine is created or you can use the standard ```vagrant``` user.  
Run:

```bash
vagrant up
```
