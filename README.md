# Ansible generic PHP develop environment role

Simple Ansible role to deploy a security-relaxed PHP develop environment on Ubuntu Server 14.04.

- IPtables (basic security)
- SSH server (basic security)
- Nginx or Apache2
- PHP 5.6
- MySQL client
- Git
- Composer

One project per host, multiple users.

The configured users are created in the system with SSH access through their provided public SSH keys.

Nginx or Apache virtual hosts are created for every user as ```<USER>.<HOSTNAME>```. The document root of each vhost points to ```/home/<USER>/projects/<COMPANY>/<PROJECT>/web```.

The web server logs are created with read access for every user.

## Usage

1. Edit the ```hosts``` file and fill it with your hosts and projects data.

2. Edit ```php-dev-env.yml```:
  * Add the hosts to provision to the ```- hosts:``` line. E.g:
    * ```- hosts: [project-group]```
    * ```- hosts: project-dev```
  * Select the web server (nginx or apache2) in the ```web_server:``` line. E.g:
    * ```web_server: nginx```
    * ```web_server: apache2```

3. Add your users and groups to the files:
     - ```roles/common/vars/system-groups.yml```
     - ```roles/common/vars/system-users.yml```

4. Add the users public SSH keys files to the directory ```roles/common/public_keys/``` with format ```<USER>.pub```.  
   ```<USER>``` must coincide with the login name of the user (e.g: john.doe.pub).

5. Run:
    * ```ansible-playbook -i hosts php-dev-env.yml --ask-pass --become --ask-become-pass```  
    or
    * ```ansible-playbook -i hosts php-dev-env.yml -k -b -K```

## Vagrant

A Vagrantfile is provided to create a local VM (Vagrant and Virtual Box required) with ip ```192.168.33.101```, to test this playbook against it.

An ```admin``` user is added (password requested) when the machine is created. You can use the standard ```vagrant``` user too.

Usage: ```vagrant up```

## Credits / License

Credits to [Jeff Geerling - Ansible role nginx](https://github.com/geerlingguy/ansible-role-nginx).

This code is distributed under the MIT license: [LICENSE](LICENSE).
