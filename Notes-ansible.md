# Ansible
- Uses 'modules' to automate running commands to groups of servers.
- The main files are the inventory and the config file.
- We can use `ansible` to run individual commands on servers or use a playbook to group multiple commands.
- Preserves "item potency", i.e. runs a command only if not in the desired state.

## Files
In `/etc/ansible` you'll find:
- `hosts` - the list of machines to configure.
- `ansible.cfg`

## Inventory
Contains the hosts to configure organized in groups.

```sh
# A group of servers called linux
[linux]
192.168.1.10
server.example.com

# The attributes to change for group 'linux'
[linux:vars]
login_user=pi
login_password=raspberry
```

## Config File
A config file can be used to set general Ansible configuration.

```py
# ansible.cfg
# Override Ansible defaults
[defaults]
# Devault inventory file instead of /etc/ansible/hosts
INVENTORY = inventory
```

## Syntax
```sh
# -i - specify an inventory file if different from default
# -m - the module to run. If not provided, 'command' module is used
#		   which treats the arguments as commands to run.
# -a - module arguments
ansible -i <inventory-file> <group> -m <module> -a <args> -u <user>
# As user 'pi', use the 'ping' module on the group 'linux' of 'inventory'
ansible -i inventory linux -m ping -u pi

```


### Commands
Those commands to use with the `command` module (defualt if no module is specified).

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

#### Running a playbook
```sh
ansible-playbook <playbook-file>
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

### `service`
```yaml
service:
  name: ntpd
  state: started
  enabled: yes
```
