# Ansible
<!-- MarkdownTOC -->

- [General](#general)
- [Install](#install)
- [Files](#files)
- [Inventory](#inventory)
- [Config File](#config-file)
- [Syntax](#syntax)
  - [Commands](#commands)
  - [Playbook](#playbook)
    - [Syntax](#syntax-1)
    - [Variables](#variables)
    - [Running a playbook](#running-a-playbook)
- [Modules](#modules)
  - [`apt` and `yum`](#apt-and-yum)
  - [Service](#service)
  - [Copy](#copy)
  - [Block in File](#block-in-file)
  - [Patch](#patch)
  - [Cron](#cron)

<!-- /MarkdownTOC -->

## General
- Uses 'modules' to automate running commands to groups of servers.
- The main files are the inventory and the config file.
- We can use `ansible` to run individual commands on servers or use a playbook to group multiple commands.
- Ansible preserves "item potency", i.e. runs a command only if not in the desired state.

Ansible has two components:
1. Inventory: Ansible communicates with the machines it manages using an inventory file that lists the hosts. You can define groups of hosts and even subgroup hosts in a hierarchical structure.
2. Playbooks: YAML files that describe the tasks you want to perform on the hosts.

## Install
It's recommended to install Ansible via pip as it's usually more updated than the distro package manager.

```sh
pip3 install ansible
```

## Files
The default location for the files is `/etc/ansible`, but it can be changed in CLI.

The files are:
- `hosts` - inventory file: the list of machines to configure.
- `ansible.cfg`

## Inventory
- Contains the hosts to configure organized in groups.
- The SSH username and password can be entered here or in the playbook.
- The default inventory location is `/etc/ansible/hosts`

```sh
# A group of servers called linux
[linux]
192.168.1.10 ansible_user=myuser ansible_password=mypassword
server.example.com

# Alias
rp1   ansible_host=198.148.118.68`

# Another server list
[webservers]
192.168.1.50
192.168.1.51

# Hierarchy
[all_servers:children]
webservers
db_servers

# The attributes to change for group 'linux'
[linux:vars]
login_user=pi
login_password=raspberry
```

Test your inventory by pinging all hosts:

```sh
ansible all -m ping -i /path/to/inventory
```

## Config File
A config file can be used to set general Ansible configuration.

```py
# ansible.cfg
# Override Ansible defaults
[defaults]
# Devault inventory file instead of /etc/ansible/hosts
INVENTORY = inventory
# Disable deprecation warning
deprecation_warnings=False
```

## Syntax
```sh
# -i - specify an inventory file [default: /etc/ansible/hosts]
# -m - the module to run. If not provided, 'command' module is used
#		   which treats the arguments as commands to run.
# -a - module arguments
# -u - ssh user
# --list - list inventory information
# <group> - host group. Use `all` to target all hosts.
ansible -i <inventory-file> <group> -m <module> -a <args> -u <user>
# As user 'pi', use the 'ping' module on the group 'linux' of 'inventory'
ansible -i inventory linux -m ping -u pi

```


### Commands
Those commands can be used with the `command` module (defualt if no module is specified).

```sh
# List free space
free -h
```


### Playbook
A Yaml file that starts with `---`. It includes 'plays' which are a set of tasks to run.

#### Syntax

```yaml
---
  # Play
  - name: install essential packages
    # Target host. Can be `all`, a single host, or a group
    hosts: linux
    # Become the sudo user
    become: yes
    vars:
      # SSH credentials if not specified in `hosts` or command
      ansible_user: myuser
      ansible_password: mypassword
    # List of tasks to run
    tasks:
      - name: ensure nano is installed
        # Module
        apt:
            name: nano
            state: latest
        # OR short form
        apt: name=nano state=latest
      # It is possible to run commands directly.
      # Not recommended as it's not item potent (see introduction for meaning).
      - command: apt install -y nano

```

#### Variables
Variables are defined using regular Yaml syntax

```yaml
vars:
  filename: myfile.sh
```

Variables are referenced using double curly braces. If they appear at the beginning, they must be quoted.

```yaml
template:
  src: "{{ filename }}"
```

#### Running a playbook
```sh
# -i - specify inventory if not default
# --check - check playbook validity without running
ansible-playbook [OPTIONS] <playbook-file>
```

## Modules

### `apt` and `yum`
```yaml
apt:
  # Package name
  name: nano
  # Install
  state: present
  # Install/update
  state: latest
  # Uninstall
  state: absent
```

### Service
```yaml
- name: Start service httpd, if not started
  ansible.builtin.service:
    name: httpd
    state: started

- name: Stop service httpd, if started
  ansible.builtin.service:
    name: httpd
    state: stopped

- name: Restart service httpd, in all cases
  ansible.builtin.service:
    name: httpd
    state: restarted

- name: Reload service httpd, in all cases
  ansible.builtin.service:
    name: httpd
    state: reloaded

- name: Enable service httpd, and not touch the state
  ansible.builtin.service:
    name: httpd
    enabled: yes

- name: Start service foo, based on running process /usr/bin/foo
  ansible.builtin.service:
    name: foo
    pattern: /usr/bin/foo
    state: started

- name: Restart network service for interface eth0
  ansible.builtin.service:
    name: network
    state: restarted
    args: eth0
```

### Copy
```yaml
- name: Copy file with owner and permissions
  ansible.builtin.copy:
    src: /srv/myfiles/foo.conf
    dest: /etc/foo.conf
    owner: foo
    group: foo
    mode: '0644'
```

__mode__

Can be either
- specified as four digits '0644'
- specified with symbols, e.g. u+rwx, u=rw,g=r,o=r
- preserve source file permissions with `preserve`

__user and group__

When left unspecified, it uses the current user unless you are root, in which case it can preserve the previous ownership.

### Block in File
This module will insert/update/remove a block of multi-line text surrounded by customizable marker lines.

```yaml
- name: Insert/Update block and appending a new line
  ansible.builtin.blockinfile:
    path: /etc/ssh/sshd_config
    # Default: false
    append_newline: true
    # Default: false
    prepend_newline: true
    block: |
      Match User ansible-agent
      PasswordAuthentication no

- name: Insert/Update block from a file and validate it
  ansible.builtin.blockinfile:
    block: "{{ lookup('ansible.builtin.file', './local/sshd_config') }}"
    path: /etc/ssh/sshd_config
    backup: yes
    validate: /usr/sbin/sshd -T -f %s

- name: Insert/Update HTML surrounded by custom markers after <body> line
  ansible.builtin.blockinfile:
    path: /var/www/html/index.html
    marker: "<!-- {mark} ANSIBLE MANAGED BLOCK -->"
    insertafter: "<body>"
    block: |
      <h1>Welcome to {{ ansible_hostname }}</h1>
      <p>Last updated on {{ ansible_date_time.iso8601 }}</p>
```

### Patch
See https://stackoverflow.com/questions/76311145/prepend-multiline-text-to-file-with-ansible

```yaml
- name: Patch a file
  ansible.posix.patch:
    ...
```

### Cron
```yaml
- name: Run a job at 2 and 5. Creates an entry like "0 5,2 * * ls -alh > /dev/null"
  ansible.builtin.cron:
    name: "check dirs"
    minute: "0"
    hour: "5,2"
    job: "ls -alh > /dev/null"

- name: 'Remove a job. Removes any job that is prefixed by "#Ansible: an old job" from the crontab'
  ansible.builtin.cron:
    name: "an old job"
    state: absent

- name: Run on boot as root "@reboot /some/job.sh"
  ansible.builtin.cron:
    name: "a job for reboot"
    special_time: reboot
    user: root
    job: "/some/job.sh"

- name: Add env variable. Creates an entry like "PATH=..." on top of crontab
  ansible.builtin.cron:
    name: PATH
    env: yes
    job: /opt/bin:/sbin
```

