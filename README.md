# Ansible Web Application (Apache2/Nginx, PHP, MySQL, Docker) Provisioning

### Folder Structure
|  Folder | Description  |
|-|-|
| group_vars  | all variables that used in this ansible playbook defined here  |
|  roles |  roles to install/manage services in machine, default is: `common`, `apache2`, `php`, `mysql`, `docker` |
| templates  | for you machine template such as `info.php` or apache2 configuration  |

### Roles
|  Roles | Description  |
|-|-|
| common  | responsible to install and update or do general roles such as **apt-get update**  |
|  apache2 |  install apache2 as webserver, `mod_rewrite` enabled by default |
| php  | install latest php version  |
| mysql | install mysql latest version |
| docker | install docker-ce |

### Setup
Ansible will using publickey instead of password, so you have to copy your ssh keys into your machine. 
```
ssh-copy-id -i <your ssh public key> <username>@<host/ip>
```

Edit `group_vars/all.yml` for the `mysql_root_password` with your favorite editor
```
---
mysql_root_pass: <mysql-password> #MySQL Root Password
```

Edit `hosts` and add your own server
```
# vm
[vm]
127.0.0.1 ansible_ssh_user=<ssh-user> ansible_ssh_private_key_file=<private-key>
```
Finally edit `provision.yml` and modify what roles/services you need to install/manage
```
- hosts: <host>
  become: yes
  roles: 
    - common
    - apache2
    - php
    - mysql
```


#### Author
Created by Sandi Andrian, MBA 
Co-Founder Kodr and eduxa.id