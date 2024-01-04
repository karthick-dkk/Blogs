---
title: "Ansible for DevOps and Cloud"
seoTitle: "Everything about Ansible for Devops"
seoDescription: "Ansible for Devops and cloud"
datePublished: Tue Dec 26 2023 12:43:56 GMT+0000 (Coordinated Universal Time)
cuid: clqmc9emg000908jybebdeqn5
slug: ansible-for-devops-and-cloud
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/CZ9AjMGKIFI/upload/d939b3849cd1b268e3832d9f4778bf30.jpeg
tags: cloud, ansible, cloud-computing, devops, ansible-playbook

---

# What ?

Ansible is an open-source automation tool that is widely used for configuration management, application deployment, task automation, and IT orchestration. Ansible is designed to be simple, agentless, and easily extensible.

# Why ?

* **Agentless Architecture**
    
* **Simple and Human-Readable Syntax:** Ansible uses YAML
    
* **Extensibility and Modules**
    
* **Integration with Cloud Platforms**
    
* **Open Source and Active Development**
    
* **Community and Ecosystem**
    

# How to Install Ansible?

For Debian/ubuntu

```bash
sudo apt update
sudo apt install ansible
```

For RedHat/Rocky/CentOS

```bash
sudo yum update
sudo yum install ansible
```

# Usage and Commands:

## Configure Ansible SSH-KEY:

Ansible uses SSH Key to login the remote server. let's create the SSH key

* Create a SSH Key for the server.
    

```bash
#Ansible Server
ssh-keygen
```

### Method 1: Copy SSH Key

Once the Key created, copy the public key using below command

```bash
#Ansible Server
cat ~/.ssh/id_rsa.pub
```

login to Remote client ,here save the key to file called **authorized\_keys.**

```bash
#Remote Client
vim ~/.ssh/authorized_keys

<Paste_your_key_here>
```

### Method 2: Copy SSH Key using ssh-copy-id

```bash
ssh-copy-id username@IP_address
```

Once Key copied check the connection, if its working without password authentication? if works good to Go..&gt;

```bash
ssh username@<remote_host>
```

## Make Inventory File:

Inventory file is used to store the client servers information and we can add group of servers.

Example: inventory

```bash
[server_group1]

192.168.111.1

192.168.111.2

[server_group2]

192.168.111.10

192.168.111.12
```

## Ansible Execution

### Execute the simple commands: **ls**

```bash
ansible -i inventory server_group1 -m bash -a "ls"
```

* \-i --&gt; Inventory group\_name
    
* \-m --&gt; [Module](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)
    
* \-a --&gt; Arguments
    

```bash
ansible 192.168.111.1 -m command -a "date" --user admin  --ask-become-pass
```

* \-m --&gt; Ansible Module name
    
* \-a --&gt; Arguments (Linux Command)
    
* \--user --&gt; Remote client user\_name \[if you are using different user\]
    
* \--ask-become-pass --&gt; Enter for password \[only **\--user** used\]
    

### Install MariaDB using Ansible:

Write a Ansible playbook for installing MariaDB on RedHat/Rocky/Centos

save the file as ansible\_mariadb.yml

> Note: The user must need root access to perform installation task

```bash
---
- name: Install Package - Mariadb
  hosts: server_group1 # mention your host group or IP
  become: yes  # Enable privilege escalation to root
  vars:
    mariadb_version: "10.5"
  tasks:
    - name: Download mariadb_repo_setup script
      ansible.builtin.get_url:
        url: https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
        dest: /tmp/mariadb_repo_setup
        mode: '0755'
    - name: Run mariadb_repo_setup script for version 10.5
      ansible.builtin.command: /tmp/mariadb_repo_setup - mariadb-server-version={{ mariadb_version }}
    - name: Installing Mariadb packages -->
      ansible.builtin.yum:
        name: "{{ item }}"
        state: present
      loop:
        - MariaDB-server
        - MariaDB-compat
        - MariaDB-client
        - MariaDB-shared
        - MariaDB-devel
        - MariaDB-common
```

### Execute Ansible playbook:

Once the playbook created ,Execute the playbook using below

```bash
ansible-playbook ansible_mariadb.yml -i inventory
```

Thanks for reading & Follow for More ✌️

* `Hashnode -`[`https://karthick-dk.hashnode.dev`](https://karthick-dk.hashnode.dev/)
    
* `Medium` - [`https://medium.com/@karthidkk123`](https://medium.com/@karthidkk123)
    
* `LinkedIn -`[`https://www.linkedin.com/in/karthick-dkk`](https://medium.com/@karthidkk123)
    
* `Instagram` - [`https://www.instagram.com/karthick_dkk_dk`](https://medium.com/@karthidkk123)
    
* `Github -`[`https://github.com/karthick-dkk`](https://medium.com/@karthidkk123)