# Linux
<!-- MarkdownTOC -->

- [Various:](#various)
- [GUI Shortcuts:](#gui-shortcuts)
- [CLI:](#cli)
    - [Command Redirection and Pipelines](#command-redirection-and-pipelines)
    - [Directory Traversal](#directory-traversal)
    - [File linking](#file-linking)
    - [I/O](#io)
        - [Using echo to write to a file](#using-echo-to-write-to-a-file)
    - [Searching](#searching)
        - [Grep](#grep)
        - [PGrep](#pgrep)
        - [Silver Searcher](#silver-searcher)
        - [Locate](#locate)
        - [LS with wildcards](#ls-with-wildcards)
        - [Find](#find)
    - [Managing files](#managing-files)
- [User Management](#user-management)
    - [Change Hostname](#change-hostname)
    - [Changing File Permissions](#changing-file-permissions)
    - [New Sudoer User](#new-sudoer-user)
    - [Never Ask sudo Password](#never-ask-sudo-password)
- [Disk Management](#disk-management)
    - [Resize a disk image](#resize-a-disk-image)
- [Services, Logging, Journal](#services-logging-journal)
    - [systemctl](#systemctl)
    - [journalctl](#journalctl)
    - [dmesg](#dmesg)
- [Networking](#networking)
    - [Interfaces](#interfaces)
        - [Permanent static IP](#permanent-static-ip)
    - [Routing](#routing)
    - [Bridging](#bridging)
    - [Configure WiFi](#configure-wifi)
        - [WiFi with authentication](#wifi-with-authentication)
    - [Port Scanning and Pinging](#port-scanning-and-pinging)
        - [Nmap](#nmap)
    - [SS](#ss)
        - [NC \(netcat\)](#nc-netcat)
        - [Ping](#ping)
    - [TCP Dump](#tcp-dump)
    - [DNS](#dns)
    - [Firewalld](#firewalld)
    - [OpenVPN](#openvpn)
    - [Wireguard](#wireguard)
        - [Server setup](#server-setup)
        - [Adding clients to the server](#adding-clients-to-the-server)
- [Compression, Tar](#compression-tar)
- [VIM](#vim)
    - [Vim Search](#vim-search)
    - [Vim Surround](#vim-surround)
    - [Packages](#packages)
        - [Setup Vundle](#setup-vundle)
        - [Useful Plugins](#useful-plugins)
    - [NeoVim](#neovim)
        - [LazyVim Error](#lazyvim-error)
    - [VS Code Plugin](#vs-code-plugin)
- [SCP](#scp)
- [SSH](#ssh)
    - [Enabling SSH](#enabling-ssh)
    - [SSH Logs](#ssh-logs)
    - [Key Generation](#key-generation)
    - [Authorized Keys](#authorized-keys)
        - [Authorized Keys Management](#authorized-keys-management)
    - [SSH Port Forwarding](#ssh-port-forwarding)
    - [SSH Config File](#ssh-config-file)
    - [Reset SSH Keys on Oracle Cloud](#reset-ssh-keys-on-oracle-cloud)
    - [Run Script on Remote](#run-script-on-remote)
    - [Reverse SSH](#reverse-ssh)
- [Background and Detached Processes](#background-and-detached-processes)
    - [Reattached Process to Terminal](#reattached-process-to-terminal)
    - [Run in Background with Logs](#run-in-background-with-logs)
- [Auto-run commands at startup](#auto-run-commands-at-startup)
    - [rc.local](#rclocal)
    - [.bashrc .zshrc .profile](#bashrc-zshrc-profile)
    - [Upstart job \(for systems older than 15.04\) \(not recommended\)](#upstart-job-for-systems-older-than-1504-not-recommended)
    - [Init script \(obsolete\)](#init-script-obsolete)
    - [Cron](#cron)
        - [Cron Logs](#cron-logs)
- [Package Management](#package-management)
    - [rpm](#rpm)
- [Bash](#bash)
    - [Specifying shell location](#specifying-shell-location)
    - [Bash Variables](#bash-variables)
    - [Command Line Arguments](#command-line-arguments)
    - [Command Substitution](#command-substitution)
    - [Operators](#operators)
    - [Arithmetic Expansion](#arithmetic-expansion)
    - [SH list](#sh-list)
    - ['test' command](#test-command)
    - [String Manipulation](#string-manipulation)
    - [Arrays](#arrays)
    - [Flow Control](#flow-control)
        - [If..Then](#ifthen)
        - [Do...While](#dowhile)
        - [For](#for)
        - [Case](#case)
    - [Functions](#functions)
    - [Exiting the script](#exiting-the-script)
    - [Error Handling](#error-handling)
    - [Alias](#alias)
- [Makefile](#makefile)
    - [Structure](#structure)
        - [Default Target](#default-target)
    - [Line Prefixes](#line-prefixes)
    - [Variables](#variables)
    - [Flow Control](#flow-control-1)
    - [Make Functions](#make-functions)
    - [String Manipulation](#string-manipulation-1)
- [Commands](#commands)
    - [basename](#basename)
    - [dirname](#dirname)
    - [Date and time](#date-and-time)
    - [man](#man)
    - [info](#info)
- [Tools](#tools)
    - [Curl](#curl)
    - [Meg](#meg)
    - [Sed \(Linux Stream Editor\)](#sed-linux-stream-editor)
    - [AWK](#awk)
    - [Youtube Downloader](#youtube-downloader)
    - [Protoscope and Protocol Buffers](#protoscope-and-protocol-buffers)
    - [XXD hex conversion](#xxd-hex-conversion)
    - [nohup no hangup background services](#nohup-no-hangup-background-services)
    - [Tailscale](#tailscale)
    - [Tmux](#tmux)
        - [Tmux config repo](#tmux-config-repo)
        - [Tmux Issues](#tmux-issues)
- [Serial](#serial)
    - [Minicom](#minicom)
    - [Screen](#screen)
- [Raspberry](#raspberry)
    - [GPIO Control](#gpio-control)
    - [SD Card Backup](#sd-card-backup)
    - [Java for RPi](#java-for-rpi)
    - [2.5G Ethernet](#25g-ethernet)
    - [Apt Update on old OS](#apt-update-on-old-os)
- [Home Server](#home-server)
    - [Docker](#docker)
    - [Portainer](#portainer)
    - [Homer](#homer)
    - [ShellInABox](#shellinabox)
    - [Nginx Proxy Manager](#nginx-proxy-manager)
    - [Nextcloud](#nextcloud)
    - [Pihole](#pihole)
        - [WSL with Pihole](#wsl-with-pihole)
    - [Dynamic DNS](#dynamic-dns)
    - [Influxdb, Telegraf, Grafana](#influxdb-telegraf-grafana)
    - [Netdata](#netdata)
        - [Configure parent and child nodes](#configure-parent-and-child-nodes)
    - [n8n Workflow Automation](#n8n-workflow-automation)
- [Using NTFS Disks](#using-ntfs-disks)
- [OS Specific](#os-specific)
    - [Ubuntu Codename](#ubuntu-codename)
- [Software](#software)
    - [Virtual Box](#virtual-box)
    - [ROS2](#ros2)
- [Common Problems](#common-problems)

<!-- /MarkdownTOC -->

# Various:
- Tex tools for linux: texlive
    texlive texlive-latex texlive-xetex
    texlive-xetex-def
    texlive-collection-xetex
    texlive-collection-latexextra
- Running multiple commands
    A; B        => Run A and then B, regardless of success of A
    A && B      => Run B if A succeeded
    A || B      => Run B if A failed
    A &         => Run A in background.
- Create .bashrc if it does not exist:
    touch ~/.bashrc
    chmod 644 ~/.bashrc
- Add a directory to PATH:
    export PATH="/path/to/dir:$PATH"

# GUI Shortcuts:
- Lock the screen:                  CTRL-ALT-L
- Open 'nautilus' (file manager):   ALT-F2
- Show location text box:           CTRL-L
- Show hidden files and dir's:      CTRL-H
- Switch from GUI to terminal:      CTRL-ALT-F<1-7>


=====================================================================


# CLI:
- Start file manager:
    nautilus
- View all commands that have a certain string in their name
    man -f <string in command>
    whatis <string in command>
- View all commands that have <word> in their description
    man -k <word>
    apropos <word>
- Turn off the GUI
    sudo service lightdm stop
- Halt or turn off the system:
    $ shutdown -h OR $ halt OR $ poweroff   => turn off
    $ shutdown -r <now/time>                => restart
- Find installation directory of a program:
    which <program name>
    whereis <program name>      =>have a broader scope
- Print home directory:
    echo $HOME
- Print working directory:
    pwd
- Displays a tree view of the filesystem:
    tree <-d view dir only>
- Create directory:
    mkdir /tmp/dir1

## Command Redirection and Pipelines
`>` is used to redirect stdout to a file

    $ ls > file

`<` is used to let the command get its input from the source after the symbol

    $ grep searchterm < file

`>>` is used to append stdout to a file

    $ date >> file

`2>` is used to redirect stderr to a file

    $ cmd 2> file

`|` takes the stdout from the command preceding it and redirects it to the command following it

    $ ls -l | grep searchword | sort -r

## Directory Traversal
- Change directory:

    # NOTE: .(present dir), ..(parent dir), ~(home dir)
    cd  OR  cd ~        # Change to home directory
    cd -                # Change to previous directory
    cd /                # Change to root

- Push current directory in directory stack

    `pushd`

- Go to the most recent directory in in the stack

    `popd`

- View directory stack:

    `dirs`

## File linking
- Create a hard link (file2) to an existing file

    $ ln file1 <link name>

- Create a soft (symbolic) link (file2) to an existing file

    $ ln -s file1 <link name>

- Prints files with inode number in columns:

    $ ls -li

## I/O
- The three standard file streams are: stdin, stdout, stderr
- They are represented by file descriptors: 0, 1, 2
- If other files are opened, they start from discriptor 3
- Redirect stdin so we read from another file:
    $ <command> < <input-file>
- Redirect stdout to send output to a file:
    $ <command> > <output_file>
- To redirect stderr we use its description:
    $ <command> 2> <error_file>
- To redirect stdout and stderr:
    $ <command> > <all_output_file> 2>&1
- In bash it can be replace by:
    $ <command> >& <all_output_file>

### Using echo to write to a file
```sh
# Create file or overwrite it if exists
echo 'text' > file.txt
# Append
echo 'text' >> file.txt

# Write to a file that needs root
echo 'text' | sudo tee file.txt

# Append to a file that needs root
echo 'text' | sudo tee -a file.txt
# OR via a sudo shell
sudo sh -c 'echo "text" >> file.txt'
# Mute tee output
echo 'text' | sudo tee -a /file.txt > /dev/null
```

## Searching

### Grep

- Used to find a string inside files and returns the line of occurrence:
    $ grep -r word      => look for word recursively in all files in the current directory
    $ grep foo bar.txt  => look for foo in bar.txt
- Can be used to search in the output of another command using the pipe:
    $ <cmd> | grep <search_phrase>
- To grep a special character add '$' before it 
    $ grep $'\t' bar.txt

### PGrep
Similar to grep, but used to find processes.
By default, pgrep only searches the process name. The name is a truncated version of the entire command.
- `-x` - the exact pattern (no partial match)
- `-f` - the pattern is normally only matched against the process name (first 15 chars).  When -f is set, the full command line is used.


### Silver Searcher

10x faster than grep for searching for a word within files in a directory.

```sh
sudo apt install silversearcher-ag
# Basic search - list all results
ag <word> <directory>
# List each matching file and number of matches
ag --count <word> <directory>
# Create an ".ignore" with directories to ignore
echo "test" > ~/express/.ignore
# Ignore certain extensions
ag --ignore *.md <word> <directory>
```

### Locate

- Search a pre-built database for files and folders names containing a word then filter for the results that include word2:
    $ locate word | grep word2
    $ locate zip | grep bin
        > /usr/bin/gzip
- Update the search database manually:
    $ updatedb

### LS with wildcards

- Usable wildcards: `?, *, [set], [!set]`

```sh
ls ba[tlr]    # returns bat, bal or bar
ls ba[!a-s]   # accepts letters outside a-s range
```

### Find

- Find files in specific dir with specific conditions (default <directories> is `.`)
    $ find <directories> <arguments>
- Available 'find' arguments:
    * -name <file/dir name>
    * -iname <case insensitive name>
    * -type <d/f>               => find only files or only directories
    * -maxdepth <n>             => look only in n depth
    * -ctime <num/+num/-num>    => files created before exactly/greater/less than num days
    * -atime <num/+num/-num>    => for access time
    * -mtime <num/+num/-num>    => for modification time
    * -cmin/amin/mmin <+-num>   => for minutes instead of days
    * -size <+-num><c/k/M/G>    => size in byte, KB etc.
    * -perm <permission>        => find files with this permission
    * !                         => inverts the search (find not matching files)
    * -o                        => apply OR relation between the provided search criteria
- Executing a command on the found files:
    $ find <arg> -exec rm {} ';'
    NOTE: Line must end with ';' or \;
- Find and remove:
    $ find . -type f -name "*.bak" -exec rm -f {} \;
- To get a prompt before execution, use -ok instead of -exec
- Exclude 'permission denied' and error messages:
    $ find 2>/dev/null
- Examples:
    find -name 'test*'          => find files and dirs in the current dir that start with 'test'
    find .. -name test\*        => find files and dirs in the parent dir that start with 'test'
    find -name 'abc*' -name '*.php'     => find files that start with 'abc' and end with 'php'
    find -name 'abc*' ! -name '*.php'   => find files that start with 'abc' and doesn't end with 'php'
    find -name 'abc*' -o -name '*.php'  => find files that start with 'abc' or end with 'php'
    find ./t1 ./t2 -name 'abc*'         => find in mulitple directories
    find -type f -perm 0664             => find all files with this permission
    find / -size +50M -size -100M       => find files with sizes b/w 50-100MB
    find -type f -exec ls -s {} \; | sort -nr | head -5 => find the largest 5 files


## Managing files
- Viewing files:
    $ cat <file>            => view with no scroll-back
    $ tac <file>            => view backwards
    $ head <file> [-<num>]  => view the first 10 (or num) lines
    $ tail <file> [-<num>]  => view the last 10 (or num) lines
    $ less <file>   => view page by page with search and navigation
    NOTE: Use / to search forward, ? to search backward
- Change a file's time stamp or create one if not existed
    $ touch <filename> <arg>
    * -t 03201600       => set time stamp to 4pm 20/3
- Create a directory
    $ mkdir <name or path+name>
- Removing a directory (it must be empty):
    $ rmdir <dir>
- Removing a directory and its contents:
    $ rm -rf <dir>
- Sort lines of a file:
    $ sort <file>
- Print unique lines of a file:
    $ uniq -u <file>

_______________________________________________________________________________
# User Management

Add user to group

```sh
usermod -a -G mygroup myuser
```

List all members of a group

```sh
getent group mygroup
```

## Change Hostname
Edit the oldname in these files:

```sh
sudo nano /etc/hostname
sudo nano /etc/hosts
```

Even easier, use this command:

```sh
hostnamectl set-hostname my_host
```

## Changing File Permissions
`chmod` is used to control file privileges

- Each permission setting can be represented by a numerical value:
    r = 4   w = 2   x = 1   - = 0
- Example:
    u(ser)  g(roup) o(others)
    (rw-)   (rw-)   (r--)
    4+2+0   4+2+0   4+0+0
    chmod 664 sneakers.txt

```sh
# Add read/write/execute privilege to user (owner)
$ chmod u+rwx test.txt

# Mark the file as executable
$ chmod +x myscript.sh
```

## New Sudoer User
```sh
# Create new user
sudo adduser ubilogix
# Add the user to sudo group
sudo adduser ubilogix sudo
```

## Never Ask sudo Password
Open a Terminal window and type:

```sh
sudo visudo
```

In the bottom of the file, add the following line:

```sh
<username> ALL=(ALL) NOPASSWD: ALL
```

_______________________________________________________________________________
# Disk Management

## Resize a disk image
Let's say the `dd` has been used to create an image of 32GB disk. If we just restore the image to a 16GB it will fail even if the actual data content is less.
To achieve that we have to shrink the image first.

```sh
# Enable the loopback:
sudo modprobe loop

# Request a new (free) loopback device:
sudo losetup -f

# The command returns the path to a free loopback device:
/dev/loop0

# Create a device of the image:
sudo losetup /dev/loop0 myimage.img

# The device /dev/loop0 represents myimage.img. We want to access the partitions that are on the image, so we need to ask the kernel to load those too:
sudo partprobe /dev/loop0

# This should give us the device /dev/loop0p1, which represents the first partition in myimage.img. We do not need this device directly, but GParted requires it.

# Resize partition using GParted:
# Load the new device using GParted:
sudo gparted /dev/loop0
```

_______________________________________________________________________________
# Services, Logging, Journal

## systemctl
Manage systemd services.

```sh
systemctl status service-name
systemctl start service-name
systemctl stop service-name
systemctl restart service-name
# Enable/disable service on boot
systemctl enable service-name
systemctl disable service-name
# Reload service config without restarting it
systemctl reload service-name
```

## journalctl
See systemctl service logs

```sh
# Logs of a specific unit (service)
journalctl -u service-name
# only log messages for the current boot:
journalctl -u service-name -b
# Follow log
journalctl -f
```

## dmesg
View kernel logs. Useful for:
- Hardware and kernel issues.
- OOM killer.

```sh
dmesg
```

_______________________________________________________________________________
# Networking

## Interfaces

```sh
# View the current interface configuration:
ifconfig

# Change the IP of a certain interface:
ifconfig <interface> <ip> netmask <subnetmask)> broadcast <broadcast_ip>
ifconfig eth0 10.10.11.30 netmask 255.255.255.0 broadcast 10.10.11.255
ifconfig eth0 10.10.11.30/24
# The default interface configuration can be changed in /etc/netwrok/interfaces
# To set the interface eth0 to use DHCP:
iface eth0 inet dhcp
# To set a static IP to interface eth0:
iface eth0 inet static
    address <ip>
    netmask <ip>
    gateway <ip>
```

### Permanent static IP
(Debian) Modify `/etc/dhcpcd.conf`:

```sh
interface eth0
static ip_address=172.31.1.69/24
static ip6_address=fd51:42f8:caae:d92e::ff/64
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8.8 fd51:42f8:caae:d92e::1
```

## Routing
Add an entry to the routing table

```sh
# Add default route
sudo route add default gw <IP> <interface>

# Delete default route
sudo route delete default
# To delete a specific default
sudo route delete default gw <IP> <interface>
route del 10.120.100.0 eth0

# To modify a route, you have to delete it and add it again
ip route del 172.31.1.0/24 via 30.1.2.2
ip route add 172.31.1.0/24 via 172.31.1.69 metric 0
ip route add 10.2.0.0/24 via 7.0.0.1 dev sim0
```

## Bridging
We need bridge-utils

```sh
sudo apt install bridge-utils
```

Create the bridge and add each interface to it

```sh
brctl addbr br0
brctl addif br0 eth1
brctl addif br0 eth2
# Bring up the interfaces and bridge
ifconfig eth1 0.0.0.0
ifconfig eth2 0.0.0.0
ifconfig br0 up
```



## Configure WiFi
Scan available networks (assuming `wlan0` is the interface name):

```sh
sudo iwlist wlan0 scan
```

Open the `wpa-supplicant` configuration file

```sh
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

Add you SSID and password to

```
network={
    ssid="testing"
    psk="testingPassword"
}
```

### WiFi with authentication
```sh
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
# Add
country=NO
network={
    ssid="eduroam"
    proto=RSN
    key_mgmt=WPA-EAP
    pairwise=CCMP
    auth_alg=OPEN
    eap=PEAP
    identity="haavape@ntnu.no"
    password="Guitarhero95"
    ca_cert="/etc/ssl/certs/eduroam.pem"
    phase1="Peaplabel=0"
    phase2="auth=MSCHAPV2"
    priority=1
}

sudo nano /etc/dhcpcd.conf
# Add
interface  wlan0
env  ifwireless = 1
env  wpa_supplicant_driver = wext , nl80211
```

## Port Scanning and Pinging

### Nmap
```sh
# Scan an IP for open ports
nmap -sT 254.12.132.165
# Scan a subnet for open ports
nmap -sT 192.168.1.0/24
# Scan for vulnerability
nmap --script vuln 254.12.132.165

# Other options
-O    # Show operating system
```

## SS

```sh
# Check port usage
ss -tulpn | grep :80
```

### NC (netcat)
```sh
# Ping a single port
nc -vz <remote-host> <port>
# Port scanning
nc -vz aarvik.dk 1-100
```

### Ping
```sh
# i - interval between packets (sec). Sudo needed for interval < 2ms
# c - end 128 packets
# q - only show summary
sudo ping -i 0 -c 128 -q 1.1.1.1
ping -i 0.002 -c 128 -q 1.1.1.1
```

Include timestamp in ping message

```sh
ping 1.1.1.1 | while read pong; do echo "$(date): $pong"; done
```

## TCP Dump

```sh
# List available interfaces
sudo tcpdump -D
# Capture
sudo tcpdump -i <interface> [filters]
# Other options
-n                  disable name resolution
-nn                 disable port resolution
-c <count>          capture only a number of packets
-X                  Print packet contents in hex
-A                  Print packet contents in ascii
-w <filename.pcap>  Save capture to a file. Use -v to also display on screen.
-r <filename.pcap>  Reaed a file saved earlier
# Filters
host <ip>   Limit capture to only packets related to a specific host
src <ip>    Limit capture to only packets from to a specific host
dst <ip>    Limit capture to only packets to to a specific host
port <port> Limit to packets on a certain port
icmp
# Complex filter
sudo tcpdump -i any -c5 -nn "port 80 and (src 192.168.122.98 or src 54.204.39.132)"
```

## DNS
```sh
# Lookup
nslookup google.com
dig google.com
# Query specific server
dig @8.8.8.8 google.com
# Resolve config
cat /etc/resolv.conf

# Resolv daemon status
systemctl status systemd-resolved
```

## Firewalld
The firewalld daemon manages groups of rules using entities called “zones”. Zones are basically sets of rules dictating what traffic should be allowed depending on the level of trust you have in the networks your computer is connected to. Network interfaces are assigned a zone to dictate the behavior that the firewall should allow.
All interfaces are assigned to a default zone until reassigned by the user.

<https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7>

```sh
# Commands apply to the default zone unless the flag `--zone=...` is used.

# Check the default firewalld zone
firewall-cmd --get-default-zone

# Print default zone config
sudo firewall-cmd --list-all

# Print config for all zones
sudo firewall-cmd --list-all-zones

# List available services
# Service definitions are found at: /usr/lib/firewalld/services/ssh.xml
firewall-cmd --get-services

# Add a an existing service to a zone
sudo firewall-cmd --permanent --add-service=http

# Add the port to the default zone (requires restart to take effect)
sudo firewall-cmd --permanent --add-port=1883/tcp
```

## OpenVPN
(Debian) Install

```sh
sudo apt install apt-transport-https
wget https://swupdate.openvpn.net/repos/openvpn-repo-pkg-key.pub
sudo apt-key add openvpn-repo-pkg-key.pub
sudo wget -O /etc/apt/sources.list.d/openvpn3.list https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-buster.list
sudo apt update
sudo apt install openvpn3
```

Usage

```sh
openvpn3 session-start --config ${MY_CONFIGURATION_FILE}
openvpn3 sessions-list
openvpn3 session-manage --config ${CONFIGURATION_PROFILE_NAME} --restart
openvpn3 session-manage --config ${CONFIGURATION_PROFILE_NAME} --disconnect
```

## Wireguard
### Server setup
__On Linux__

```sh
# Restrict permissions of created files and directories
umask 077
# Generate public and private keys for the server
wg genkey | tee /etc/wireguard/privatekey | wg pubkey > /etc/wireguard/publickey  
```


__On Windows__

Add an empty tunnel. Private and public keys will be auto-generated. Add the server address and an optional port (default is 51820)
```sh
[Interface]
Address = 10.254.0.1/24
ListenPort = 49312
```

### Adding clients to the server
First, generate the client keys. In command prompt:

```sh
wg genkey > client.key
type client.key | wg pubkey > client.pub
wg genpsk > client.psk
```

Create a file `client.conf` with the following info.

```sh
[Interface]
# From client.key
PrivateKey = xxx
# Client address
Address = 10.254.0.2/32

[Peer]
# Public IP of the server
Endpoint = 10.6.66.76:49312
AllowedIPs = 0.0.0.0/0, ::/0
# From the server config
PublicKey = yyy
# From client.psk
PresharedKey = zzz
```

Add the client info to the server config file.

```sh
[Peer]
AllowedIPs = 0.0.0.0/0, ::/0
# From client.pub
PublicKey = 
# From client.psk
PresharedKey = 
```
_______________________________________________________________________________
# Compression, Tar

_Note_: On Mac use `gtar` (`brew install gnu-tar`). 

```sh
# Compress
tar -czvf <output_file> <target_to_compress>
tar -czvf projects.tar.gz $HOME/projects/

# Decompress
tar -xvf <file>

# View oontents
tar -tf file.tgz
```

```
-c  Create a new archive
-x  Extract files from an archive
-t  List the contents of an archive
-v  Verbose output
-f file.tar.gz  Use archive file
-C DIR  Change to DIR before performing any operations
-z  Filter the archive through gzip i.e. compress or decompress archive
```

_______________________________________________________________________________
# VIM
- Piping stdout to vim:
    $ grep foo bar.txt | vim - 
- Run vim command (that starts with ':') from command line
    $ vim <file> -c <cmd>
    $ vim foo.cpp -c wq
- Options
    Options are set with `:set <option>` and disabled with `:set no<option>`.

    number             Show line number
    ic, ignorecase     ignore case for search
    hls, hlsearch           highlight search matches

```
Motions
    h, j, k, l      move left, down, up, right
    w/W             jump to the start of next word/big word
    e/E             jump to the end of next word/big word
    $               end of line
    gg              start of file
    G               end of file
    CTRL+g          line information
    <num>gg/G       jump to line
    CTRL+o          previous cursor location
    CTRL+i          next cursor location
    %( %[ %{        jump to matching parentheses

Commands
    i                   enter insert mode at current character
    I                   enter insert mode at start of line
    a                   enter insert mode at next character
    A                   enter insert mode at end of line
    R                   enter replace mode
    vi<marker>          select text inside the specified marker
        vib/vi(, viB/vi{, vi[, vi', vi"
    va<marker>          same as `vi` but includes the marker
    y<mod>              yank (copy) y-line w-word 
    d<mod>              delete (cut) d-line w-word 3down-delete 3 lines down
    p                   put (paste)
    r<char>             replace the chatacter under courser with char
    u                   undo
    ctrl+r              redo
    c<mod>              change
        ce              delete until the end of the word, start insert mode
        cc              delete the whole line, start insert mode
        c<delete motions>
    o                   open a new line bellow and enter insert mode
    O                   open a new line above and enter insert mode

Marks
    ma              create a bookmark 'a'. The label can be lower or upper case.
                    Lower case label: same file. Upper case: across files
    `a              jump to bookmark position
    'a              jump to bookmark line
    d'a             delete from current line to line of mark a
    d`a             delete from current cursor position to position of mark a
    c'a             change text from current line to line of mark a
    y`a             yank text to unnamed buffer from cursor to position of mark a
    :marks          list all the current marks
    :marks aB       list marks a, B
```
- Tab
    If you're in insert mode:
        Ctrl+d - shift left
        Ctrl+t - shift right
    If you're in normal mode:
        Shift+<< - shift current line left
        Shift+>> - shift current line right
    If you're in visual mode and have 1 or more lines selected:
        '<' - shift selection left
        '>' + shift selection right

## Vim Search
(http://vim.wikia.com/wiki/Search_and_replace)

__Search__

    *                   search for the word under cursor
    /foo                search for 'foo'
    ?foo                search in the backward direction
    n                   next search result
    N                   previous search result
    <phrase>/ignore\c   ignore case

__Search and replace__

    :s/foo/bar/g        Change each 'foo' to 'bar' in the current line.
    :%s/foo/bar/g       Change each 'foo' to 'bar' in all the lines.
    :%s/\t/  /g         Replace tabs with spaces
    :%s/foo/bar/gc      Change each 'foo' to 'bar', but ask for confirmation first.
    :.,$s/foo/bar/g     Change each 'foo' to 'bar' for all lines from the current line (.) to the last line ($) inclusive.
    :.,+2s/foo/bar/g    Change each 'foo' to 'bar' for the current line (.) and the next 2 lines (+2).
    :%s//bar/g          Replace each match of the last search pattern with 'bar'.

## Vim Surround
__Normal mode__

y s <motion> <delimiter>
ysw" -> surround word    
ysiw" -> surrounding the word independent of the cursor

__Visual mode__

After making the selection just use `S <delimiter>`

## Packages
### Setup Vundle
```sh
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

```vim
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" Plugins go here

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```

After adding your plugins in `.vimrc` run `:PluginInstall`.

### Useful Plugins

```sh
# Powerline
Plugin 'Lokaltog/powerline', {'rtp': 'powerline/bindings/vim/'}
# Install
sudo apt install powerline

# Syntax highlighting and linting (slow on Pi)
Plugin 'dense-analysis/ale'
# Multi cursor
Plugin 'terryma/vim-multiple-cursors'
```

## NeoVim
Installation:

```sh
# Linux
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
chmod u+x nvim.appimage
./nvim.appimage
# If the ./nvim.appimage command fails, try:
./nvim.appimage --appimage-extract
./squashfs-root/AppRun --version

# MacOS
brew install neovim

sudo cp ./nvim.appimage /usr/local/bin/nvim
sudo chmod 755 /usr/local/bin/nvim
```

### LazyVim Error
If you get "Failed to source" error on LazyVim startup, run the following:

```sh
find ~/.config/nvim -type f -exec dos2unix {} \;
find ~/.local/share/nvim -type f -exec dos2unix {} \;
```

## VS Code Plugin
Use default behaviour for keybindings.

```json
"vim.handleKeys": {
    "<C-p>": false,
}
```
_______________________________________________________________________________
# SCP
- Copy the file "foobar.txt" from a remote host to the local host
    $ scp your_username@remotehost.edu:foobar.txt /some/local/directory
- Copy the file "foobar.txt" from the local host to a remote host
    $ scp foobar.txt your_username@remotehost.edu:/some/remote/directory
- To copy a directory add -r

# SSH

## Enabling SSH
```sh
sudo update-rc.d ssh enable
sudo service ssh start
```

## SSH Logs
```sh
journalctl -t sshd
# Since last boot and in reverse order
 journalctl -t sshd -b0 -r
```

## Key Generation
Generate your ssh-rsa key using an email as a label:

```sh
ssh-keygen -t rsa -b 4096 -C "custom_label"
```

## Authorized Keys
- Copy the key which gets stored in `~/.ssh/id_rsa.pub`
- Login to the remote server
- Paste the file contents in `~/.ssh/authorized_keys`

or

```sh
cat ~/.ssh/id_rsa.pub | ssh pi@192.168.0.11 'cat >> .ssh/authorized_keys'
```

or

```sh
ssh-copy-id pi@192.168.0.11
```

### Authorized Keys Management
https://gist.github.com/sivel/c68f601137ef9063efd7

- Add all the public keys to a file
- Use Nginx to host the file
- Write a script to fetch the file from the server and place it in `/usr/local/bin/userkeys.sh`. `$1` is the SSH username.

```sh
#!/bin/bash
curl -sf https://keyserver.example.org/users/$1/keys
```

- Set file permissions

```sh
sudo chmod 755 /usr/local/bin/userkeys.sh
```

- Verify that `nobody` can run the file

```sh
sudo -su nobody
/usr/local/bin/userkeys.sh
```

- Configure `/etc/ssh/sshd_config`. `AuthorizedKeysCommand` passes the username to the command

```sh
AuthorizedKeysCommand      /usr/local/bin/userkeys.sh
AuthorizedKeysCommandUser  nobody
```

- Restart the SSH daemon

```sh
/etc/init.d/ssh restart
```


## SSH Port Forwarding
```sh
ssh -NL <REMOTE_PORT>:localhost:<LOCAL_PORT> <SERVER_USER>@<SERVER_IP>
ssh -NL 1883:127.0.0.1:1883 fh@192.168.1.111
# Run in the background
ssh -fNL 1883:127.0.0.1:1883 fh@192.168.1.111

```

## SSH Config File
Add the following in `~/.ssh/config`

```sh
# Just an alias
Host mybox
  HostName 10.10.107.241
  User root
# Optional fields
  Port 47150
  IdentityFile /Users/jon/.ssh/id_rsa_4096
  LocalForward 8081 127.0.0.1:8081

# Port forwarding
Host 16.10/port6
  HostName port6
  User root
  ProxyCommand ssh -W %h:%p root@10.10.16.10

# ProxyJump
# Allows to get to userB@ServerB that is accessible via userA@ServerA
Host mybox
  HostName ServerB
  User userB
  ProxyJump userA@ServerA
```

## Reset SSH Keys on Oracle Cloud
- Login to Oracle Cloud
- Launch a console connection
- Reboot the instance
- Press 'up' arrow during reboot until kernel selection show up.
- Press 'e' to edit the run script.
- Add `rw init=/bin/bash` to the end of the line starting with `linuxefi`.
- Exit and save by pressing `ctrl+x`.
- Run the following commands.

```sh
/usr/sbin/load_policy -i
/bin/mount -o remount, rw /
cd ~opc/.ssh
mv authorized_keys authorized_keys.old
# Add the desired public key
vim authorized_keys
chmod 600 authorized_keys
chown opc:opc authorized_keys
/usr/sbin/reboot -f
```

## Run Script on Remote
```sh
# Local script (no args)
ssh user@remote 'bash -s' < script.sh
# Remote script
ssh user@remote '~/run --name jon'
```

## Reverse SSH


___
# Background and Detached Processes
## Reattached Process to Terminal
__Using reptyr__

```sh
reptyr PID
```

__Using screen__

```sh
screen -S session_name    # Start a new screen session with a name
your_command > logfile.txt 2>&1   # Run your command, output to file
# Press Ctrl-A, then D to detach from the session

# To reattach:
screen -r session_name
```

## Run in Background with Logs
__&__

Note that closing the terminal would also terminate the process.

```sh
your_command > logfile.txt 2>&1 &
```
__tee__

If you want to both see the output on the console and write it to a file at the same time, you can use the `tee` command. This will allow you to see the output in real-time and also save it to logfile.txt. If you close the terminal or it gets disconnected, however, you won't see the output unless you were using screen or tmux.

```sh
your_command 2>&1 | tee logfile.txt &
```

__nohup__

Combining `nohup` with `tail -f` can keep your process running independently of the terminal session, and you can monitor the output in real-time from another terminal:


```sh
nohup your_command > logfile.txt 2>&1 &
tail -f logfile.txt
```


_______________________________________________________________________________
# Auto-run commands at startup
## rc.local
Run at startup:
Add the commands to `/etc/rc.local` before `exit 0`.

## .bashrc .zshrc .profile

_.profile_

- Run only once at system login (for bash and certain other shells - not zsh).
- Use for:
    * one-time setup, things things that are not shell-specific like environment variables.
    * programs that you want to run once when you log in or for the whole session


_.bash_profile_

- Overrides .profile if present

_.zprofile_

- .profile equivalent for zsh

_.bashrc & .zsh_

- Sourced by every sub-shell
- Use for per-shell stuff like such as aliases and function definitions, shell option settings, completion settings, prompt settings, key bindings, etc.


## Upstart job (for systems older than 15.04) (not recommended)
Create `/etc/init/myjob.conf` with content like the following

```sh
description     "my job"
start on startup
task
exec /path/to/my/script.sh
```

## Init script (obsolete)
Create a new script in /etc/init.d/myscript.

```sh
vi /etc/init.d/myscript
# Configure the init system to run this script at startup.
update-rc.d myscript defaults
```

## Cron
- `crontab -e` - open the cron config file
- `crontab -l` - list current jobs

```sh
# Job definition format:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  *  command

# Run every day at 1:00
00 01 * * mon-fri /usr/local/bin/rsbu -vbd1
# Run every three months
30 15 1 1,4,7,10 * /usr/local/bin/reports.sh
# Run every hour at xx:01 between 9-17 inclusive
01 09-17 * * * /usr/local/bin/hourlyreminder.sh
# Multiple ranges
0 0-8,17-23 * * * script.sh
# */x can be used to run every x, i.e. when time is divisible by x.
# Run every 5 min, every 2 hours between 8 and 18
*/5 08-18/2 * * * /usr/local/bin/mycronjob.sh

59 */3 * * * /home/pi/git/ProfileViewer/profile_viewer_kivy/venv_bot/bin/python3 /home/pi/git/ProfileViewer/profile_viewer_kivy/bot_filter_notifier.py > /home/pi/bot_filter_notifier.log 2>&1

# Special times
@reboot script.sh
```

__IMPORTANT__

Cron does not use the user environment variables. To make sure commands run as expected, their full path must be provided or PATH should be set properly.
_Note:_ You have to set all paths. Writing `PATH="xxx:$PATH"` will not work!

```sh
# In crontab -e
PATH=/bin:/usr/bin:/sbin
```

### Cron Logs
```sh
grep CRON /var/log/syslog
```

_______________________________________________________________________________
# Package Management

## rpm
Install package
    rpm -i <file_name>
Uninstall package
    rpm -e <package_name>
List installed packages
    rpm -qa
Display package information
    rpm -ql <package_name>

/********************************************************/
/*********************** Docker *************************/
/********************************************************/
Remove containers older than one week
    docker ps -a | grep 'weeks ago' | awk '{print $1}' | xargs --no-run-if-empty docker rm

/********************************************************/
/******************* Installing LaTex *******************/
/********************************************************/
- Install TexLive from https://www.tug.org/texlive/acquire.html not from apt-get
- Install missing packages from tlmgr. First you need to initialize it:
        tlmgr init-usertree
        tlmgr update --all
        tlmgr install <package_name>
- Example: Installing tikz:
    sudo tlmgr install pgf
    sudo tlmgr install tikz-cd

/********************************************************/
/********************** Setup VNC ***********************/
/********************************************************/

```sh
# Install vnc server
sudo dnf install tigervnc-server -y
# Start server
vncserver :1 -geometry 1024x768 -depth 24
# List active sessions
vncserver -list
# Use a vnc client to connect to SERVER_IP:SESSION_ID
```

/********************************************************/
/********************* Ubuntu/Mint **********************/
/********************************************************/
- Install latest git version:
    sudo add-apt-repository ppa:git-core/ppa
    sudo apt-get update
    sudo apt-get install git
- Install Ubuntu Software Center on Mint
    - Install synaptic
        sudo apt-get install synaptic
    - Install xpian-tools from synaptic
    - If "No such file or directory" error appears create the directory:
        sudo mkdir /var/cache/software-center/xapian
    - From synaptic install software-center
    - Set DISTRIB_ID=Ubuntu in /etc/lsb-release
    - To forbid the system from resetting the file upon reboot, set the file’s immutable flag
        sudo chattr +i /etc/lsb-release
    - To revert the file to editable mode
        sudo chattr -i /etc/lsb-release
    - If it still gives problems reinstall it with purge:
        sudo apt-get remove --purge software-center
        sudo apt-get install software-center
        
| apt-get |
 - Search for an installed package
    sudo apt-cache search tex*


_______________________________________________________________________________
# Bash

## Specifying shell location
- Lines starting with # are treated as comments except for the first line.
- The shell path can be specified in the first line as:
    #!/path/to/shell

## Bash Variables
- Definition
    var=value_without_spaces
    var="value with spaces"
    var=$(command)
    var=`command`
    var="$foo bar"
    var="{$foo}bar"
- Usage
    - Variables are referenced as $var_name
    - Variables can be referenced within double quotes
        echo $var
        echo "$var1 is first"
    - Strings with singles quoted are treated literally
        echo '$var'     # ($var) is printed
    - Single quotes are useful for sending commands to a file or a stream
        # Write commands to a file, make it executable and run it
        echo 'msg="Hello World!"' > hello
        echo 'echo $msg' >> hello
        chmod 700 hello
        ./hello
    - Variables may be referenced like ${var} to place them beside other chars
        echo "${var}xxx"


## Command Line Arguments
- The command line arguments are enumerated in as $0, $1 .. $9
- $0 is special in that it corresponds to the name of the script itself.
- To reference arguments after 9 they must be enclosed in brackets as ${nn}.
- 'shift' command is used to shift the arguments 1 variable to the left so that $2 becomes $1, $1 becomes $0 and so on.
- Special built in variables:
    - `$#` represents the parameter count. 
    Useful for controlling loop constructs that need to process each parameter.
    - `$@` expands to all the parameters separated by spaces. 
    Useful for passing all the parameters to some other function or program.
    - `$-` expands to the flags(options) the shell was invoked with. 
    Useful for controlling program flow based on the flags set.
    - `$$` expands to the process id of the shell innovated to run the script. 
    Useful for creating unique temporary filenames.


## Command Substitution
- A command can be substituted with its output by enclosing it as $(cmd) or using back quotes `cmd`

## Operators
```
Bash Operator   Operator    Description
-eq             ==          Equal
-ne             !=          Not equal
-gt             >           Greater than
-ge             >=          Greater than or equal
-lt             <           Less than
-le             <=          Less than or equal
-z              == null     Is null
```

## Arithmetic Expansion
Can be written in the form $((expression))

```sh
echo $((1 + 3 + 4))
echo $(($num1 + num2))
```

## SH list
A sequence of zero or more commands separated by newlines, semicolons or '&'

## 'test' command
- Exit with the status determined by EXPRESSION. It can be used in two ways:
    test OPTIONS EXPRESSION
    [ OPTIONS EXPRESSION ]

```bash
( EXPRESSION )              # EXPRESSION is true
! EXPRESSION                # EXPRESSION is false
EXPRESSION1 -a EXPRESSION2       # both EXPRESSION1 and EXPRESSION2 are true
EXPRESSION1 -o EXPRESSION2       # either EXPRESSION1 or EXPRESSION2 is true
STRING                      # the length of STRING is nonzero
-z STRING                   # the length of STRING is zero
STRING1 = STRING2           # the strings are equal
STRING1 != STRING2          # the strings are not equal
INTEGER1 -eq INTEGER2       # INTEGER1 is equal to INTEGER2
INTEGER1 -ge INTEGER2       # INTEGER1 is greater than or equal to INTEGER2
INTEGER1 -gt INTEGER2       # INTEGER1 is greater than INTEGER2
INTEGER1 -le INTEGER2       # INTEGER1 is less than or equal to INTEGER2
INTEGER1 -lt INTEGER2       # INTEGER1 is less than INTEGER2
INTEGER1 -ne INTEGER2       # INTEGER1 is not equal to INTEGER2
```

- Examples
    ```sh
    # Check if a file exists

    # Check if a directoroy exists
    # string operations
    test $var = "1" 
    [ $var != "1" ]
    # integer operations
    [ $var -eq 1 ]      # other options: -ne, -ge, -gt, -le, -lt
    # File exists
    [ -f $file ]        # -d $dir , -e $file_or_dir
    # Negation
    [ ! -f $file ]
    ```

## String Manipulation
```sh
# Non-POSIX
# Replace the first occurrence of a pattern with a given string
${parameter/pattern/string}
# Replace all occurrences of a pattern with a given string
${parameter//pattern/string}

# POSIX compliant
# Replace
echo "hello-world" | tr '-' '~'         # hello~world
# Delete
echo "  needs-trimming  " | tr -d ' '
# Substring
echo "abcdefghi" | cut -c2-6            # bcdef
# Split
echo "my-nice-pics" | cut -d'-' -f 2    # nice

```

## Arrays

```sh
# Creation
array1=(one two three four [5]=five)
array2[0]=0
array2[15]=15

# Usage
echo ${arr[0]} ${arr[1]}

${arr[*]}         # All of the items in the array
${!arr[*]}        # All of the indexes in the array
${#arr[*]}        # Number of items in the array
${#arr[0]}        # Length of item zero

echo "Array size: ${#array[*]}"

echo "Array items:"
for item in ${array[*]}
do
    printf "   %s\n" $item
done

echo "Array indexes:"
for index in ${!array[*]}
do
    printf "   %d\n" $index
done
```

## Flow Control

### If..Then
- Syntax
    if list
    then list 
    [elif list
    then list] ...
    [else list]
    fi
- The execution depends on the exit status of 'list'
- The 'test' command is usually used for the condition list
- The usage of conditions is illustrated in the following example
(spaces between if, [, ], operators and values must be used as shown)
    if [ "$1" = "1"] || [ "$1" = "2" ]
    then
       echo "The first choice is nice"
    elif [ "$1" = "3"] && [ "$2" = "4" ]
    then
       echo "The second choice is just as nice"
    elif [ "$1" = "3" ]
    then
       echo "The third choice is excellent"
    else
       echo "I see you were wise enough not to choose"
    fi
- One-liner:
    if [ ${found[pin]} != 0 ]; then echo Found $pin; fi


### Do...While
- Syntax
    while list
    do list
    done
- 'do..until' is used by replacing 'while' with 'until'
- Example:
    count=$1                        # Initialize count to first parameter 
    while [ $count -gt 0 ]          # while count is greater than 10 do
    do
       echo $count seconds left
       count=$(expr $count -1)      # decrement count by 1
       sleep 1                      # sleep for a second 
    done


### For
- Syntax
    for variable in word
    do list
    done
- A word is a variable that contains a list of values of some sort
- 'do' and 'done' may be replaced by '{' and '}'. This is not allowed for while.
- Example:
fruitlist="Apple Pear Tomato Peach Grape"
for fruit in $fruitlist
do
   if [ "$fruit" = "Tomato" ] || [ "$fruit" = "Peach" ]
   then
      echo "I like ${fruit}es"
   fi
done


### Case
- Syntax
    case word in
    pattern) list ;;
    ...
    esac
- '*' represents any pattern.
- Example:
    case $1
    in
    1) echo 'First Choice';;
    2) echo 'Second Choice';;
    *) echo 'Other Choice';;
    esac

## Functions
- Syntax
        name ( ) command
    OR
        name() {
        commands
        return $exit_status     # Optional
        }

*Return Value*

Bash functions do not allow to return a value to the caller. The `return` statement specifies the function's status code, which is a numeric value like the value specified in an exit statement. The status value is stored in the `$?` variable. If a function does not contain a return statement, its status is set based on the status of the last statement executed in the function.

- Variables can be defined locally within a function using local name=value.
- Example:
    sum() {
       echo $(($1 + $2))
    }


## Exiting the script
```bash
# Specific exit status
exit $exit_code

# Exit with status of last command.
exit
# Same as
exit $?
```

## Error Handling
To terminate a script if any command fails (exit status != 0):

```bash
trap "exit 1" ERR
```

## Alias
```bash
alias wr=”cd /var/www/html”
```

_______________________________________________________________________________
_______________________________________________________________________________

# Makefile

## Structure
Makefiles are made of _targets_ which have _prerequisites_ and runs a _recipe_.

```mak
target: prerequisites
<TAB> recipe
```

### Default Target
The first target in makefile is the default target. Meaning it will be executed if you run `make` without specifying a target.

To specify a custom default target, we can define a phony target called `.DEFAULT_GOAL`:

```mak
.DEFAULT_GOAL := install
```

A common practice is to define a phony target `all` that runs several other targets:

```mak
all: clean install
```

## Line Prefixes
They control the behaviour of make for the tagged command lines:
- `@` suppresses the normal 'echo' of the command that is executed.
- `-` means ignore the exit status of the command that is executed (normally, a non-zero exit status would stop that part of the build).
- `+` negates the effect of `-n`, `-t`, and `-q`, which basically tell make to not actually run the commands. So a line with a `+` at the front would get run anyway.

## Variables
```mak
# Evaluate the expression and assign the result to the variable
TAG=$(shell git describe --tags)
# Doesn't evaluate the expression. It will be evaluated when TAG is used
TAG=`git describe --tags`

# Using a variable
build-go:
    go build ${FLAGS}
```

## Flow Control
```mak
ifdef CATEGORY
$(info CATEGORY defined)
else
$(info CATEGORY undefined)
endif
```

## Make Functions

`$(error text…)`

Generates a fatal error where the message is `text`.

`$(warning text…)`

Prints out a warning including makefile name and line number, but `make` doesn't exit.

`$(info text…)`

Only prints the text to standard output.

`$(shell shell_command)`
``shell_command``

Evaluates a shell command and returns its output.

    contents := $(shell cat foo)

`$(wildcard pattern)`

Return all files matching `pattern`.

    SRCS := $(wildcard *.c)

## String Manipulation
```sh
# String substitution
X := $(STRINGS:%.c=%.h)  # Replace all '.c' with '.h'
# Substring
foo := $(shell git describe --tags | cut -c 1-6)
```

___
# Commands
## basename
basename - strip directory and suffix from filenames 

```sh
 basename NAME [SUFFIX]
basename /usr/bin/sort
      -> "sort"
basename include/stdio.h .h
      -> "stdio"
```

## dirname
strip last component from file name

```sh
dirname /usr/bin/
      -> "/usr"
dirname stdio.h
      -> "."
```

## Date and time
Set date from the command line

    date +%Y%m%d -s "20120418"

Set time from the command line

    date +%T -s "11:14:00"

Set time and date from the command line

    date -s "23 JUL 2021 14:14:00"
    date -s "2021-07-29 11:55:33"

## man
- Display chapter #
    man <#> <command>
- View all man pages with <word> in an their pages
    man -a <word>

## info
- 'info' is the GNU alternative to man that uses links and menus
- Syntax:
    info                    => Show topics index
    info <topic name>       => Show topic info page
- To move b/w nodes use n, p, u for next, previous and up node.

_______________________________________________________________________________
# Tools

## Curl

Queries

```sh
curl -X POST 'http://localhost:8086/query?db=mydb' --data-urlencode 'q=SELECT * FROM "mymeas"'
# Headers, data and cookies
curl -X POST "http://20.20.20.232/api/tests" \
    -H  "accept: application/json" \
    -H  "Content-Type: application/json" \
    -d "{\"identifier\":\"\",\"isMesh\":0,\"testtypeId\":5129}" \
    --cookie "PHPSESSID=3ee7b66e5e3b8d5c6892f67cd41589ab"
```

## Meg
Fetch many paths for many hosts - without killing the hosts.

```sh
# paths.txt
/api/docs
/api/swagger

# hosts.txt
https://www.site1.com
https://www.site2.com

# Command
# Verbose with 1000ms delay between calls to the same host
meg -v -d 1000 paths.txt hosts.txt meg_output
```

## Sed (Linux Stream Editor)
By default, the command result is printed to stdout.
If `-i` is used, the file is edited in-place instead.

The following commands exist:
- s: substitute
- d: delete
- i: insert before
- a: append after

```sh
# Replace the first x of each line with y
sed 's/x/y/' file.txt
# Replace all instances of x with y
sed 's/x/y/g' file.txt
# Replace nth occurance
sed 's/x/y/3' file.txt
# Replace all occurances from the nth occurance
sed 's/x/y/3g' file.txt

# Delete matching line
sed '/x/d'
# Delete blank Lines  
sed '/^$/d' file.txt
```

## AWK
```sh
# Print first and last column
awk '{print $1, NF}' log.txt
# Find lines containing string
awk '/ERR/ {print}' log.txt
```

## Youtube Downloader
https://github.com/yt-dlp/yt-dlp

```sh
yt-dlp -P <output-path> <url>
```

## Protoscope and Protocol Buffers
```sh
# Decode a binary dump
protoscope raw.bin

# Decode hexdata from a file
$ cat hexdata.txt
0a400a26747970652e676f6f676c65617069732e636f6d2f70726f746f332e546573744d65737361676512161005420e65787065637465645f76616c756500000000
$ xxd -r -p hexdata.txt | protoscope

# Decode hexdata from input
$ xxd -r -p <<< "1005420e65787065637465645f76616c756500000000" | protoscope
```

## XXD hex conversion
```sh
# Options:
# -p - plain hex string (by default uses a human readable format)
# -r - revert: hex to binary

# Binary to hex
xxd [options] file.bin
```

## nohup no hangup background services
`nohup` allows running a program in the background. It catches the hangup signal, while the ampersand doesn't.

Normally, when running a command using `&` and exiting the shell afterwards, the shell will terminate the sub-command with the hangup signal (kill -SIGHUP <pid>). This can be prevented using `nohup`, as it catches the signal and ignores it so that it never reaches the actual application.

```sh
# Run in bg
nohup my_cmd &
# Run in bg and write stdout/stderr to a file
nohup my_cmd > logfile.txt 2>&1 &
```

## Tailscale
```sh
curl -fsSL https://tailscale.com/install.sh | sh
# Add node with auth key
sudo tailscale up --authkey <my-auth-key>
# Network status
tailscale status
```

## Tmux
```sh
# Start a named session “work”
tmux new -s work
# Detach (leave everything running)
# → Ctrl‑b, then d

# List open sessions
tmux ls
# Reattach to first session
tmux attach
# Reattach to “work”
tmux attach -t work
# Kill session
tmux kill-session -t work
```

Keyboard shortcuts (all start with leader `Ctrl-b`)
```sh
c - create new window
n - switch between running windows
<n> - switch to window <n>
d   - detach session
s   - list open sessions
%   - split vertically
"   - split horizontally
:   - enter command mode
```

Commands (enter command mode with `:` first)
```sh
rename-window <name>
rename-session <name>
kill-session
```

### Tmux config repo
```sh
rm -rf ~/tmux-config
git -c core.autocrlf=false clone https://github.com/samoshkin/tmux-config.git ~/tmux-config
cd ~/tmux-config
dos2unix install.sh
bash ./install.sh
```

### Tmux Issues
```sh
##### No scroll back with mouse #####
# Add this to ~/.tmux.conf (on the remote host):
set -g mouse on
set -g history-limit 50000  # bigger scrollback per pane
# Reload (from inside tmux):
tmux source-file ~/.tmux.conf

```

_______________________________________________________________________________
# Serial

## Minicom
To exit Minicom use Ctrl+a + q

```sh
sudo minicom -D /dev/ttyUSB2
```

## Screen
```sh
# Determine baud rate
stty < /dev/ttyS0

# Open serial terminal
screen /dev/ttyS0 115200

# Exit screen
ctrl+(a \)

# Detach screen
ctrl+(ad)

# Reattach a detached screen
screen -rd

# Run with output logging (will save to screenlog.0 by default)
screen -L [-Logfile file] cmd

# Detach and run as daemon
screen -dmS name
rm screenlog.0 && screen -L -dmS simcom sudo SIM8200-M2_5G_HAT_code/Goonline/simcom-cm && sleep 2 && tail -f screenlog.0
```

_______________________________________________________________________________
# Raspberry

## GPIO Control
```sh
# Export pins (some waiting might be needed afterwards)
echo 0 > /sys/class/gpio/export
# Write to output pin
echo out > /sys/class/gpio/gpio0/direction
echo 0 > /sys/class/gpio/gpio0/value
# Read from input pin
echo in > /sys/class/gpio/gpio0/direction
cat /sys/class/gpio/gpio0/value
```

## SD Card Backup
```sh
# On MacOS: find the disk of the sd card
diskutil list
# On Linux
sudo fdisk -l
# Create and compress the image
sudo dd bs=4M if=/dev/disk2 status=progress | gzip > PiOS.img.gz
# Without compression
sudo dd bs=4M if=/dev/disk2 of=./PiOS.img conv=noerror status=progress

# Restore a compressed image
# On MacOS, you need to unmount the disk first
sudo diskutil unmountDisk disk2
gunzip --stdout PiOS.img.gz | sudo dd bs=4M of=/dev/disk2 status=progress
```

## Java for RPi
Get it from https://bell-sw.com/pages/downloads/

## 2.5G Ethernet
We need a PCIe card for CM4 and then to patch the kernel for the drivers:
https://www.youtube.com/watch?v=wCbQQ5-sjGM


## Apt Update on old OS
```sh
# Method 1 (doesn't always work)
sudo apt-get install -y --no-install-recommends dirmngr gnupg
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 \
  --recv-keys 0E98404D386FA1D9 6ED0E7B82643E131

# Method 2 - switch to archive repo on Buster
# 1) Check it's actually buster
. /etc/os-release && echo "$PRETTY_NAME"

# 2) Backup your APT sources
sudo cp /etc/apt/sources.list{,.bak-$(date +%F)}

# 3) Replace sources with the archived buster repos
sudo tee /etc/apt/sources.list >/dev/null <<'EOF'
deb http://archive.debian.org/debian buster main contrib non-free
deb http://archive.debian.org/debian-security buster/updates main contrib non-free
deb http://archive.debian.org/debian buster-updates main contrib non-free
EOF

# 4) Since archived Release files are expired, tell APT to ignore "Valid-Until"
echo 'Acquire::Check-Valid-Until "false";' | sudo tee /etc/apt/apt.conf.d/99ignore-valid-until
```

_______________________________________________________________________________
# Home Server

## Docker
```sh
curl -sSL https://get.docker.com | sh
# Add current user to docker group
sudo usermod -aG docker ${USER}
# Enable service
sudo systemctl enable docker
# The group change takes effect after logout (or reboot)
sudo reboot
# Test
docker run hello-world
```

## Portainer
Container management GUI. Use port `9000` for HTTP and `9433` for HTTPS.

```sh
docker run -d -p 9000:9000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

__Other templates__

We can use other templates to get more Protainer containers. Copy the template URL to Portainers Settings -> App Templates.

- `Protainer v2 (no OMV)` from https://github.com/SelfhostedPro/selfhosted_templates
- https://portainer-templates.as93.net
- A list of Pi OS ARM32 compatible apps is available at https://github.com/novaspirit/pi-hosted.

__Env files__

https://www.portainer.io/blog/using-env-files-in-stacks-with-portainer

__Notes__

To get the container links to work, set the right IP at Environments -> local.

## Homer
Dashboard for server apps.

```sh
docker run -d -p 8080:8080 --name=homer -v </directory/to/store/assets>:/www/assets --restart=always b4bz/homer:latest
```

Modify the config file that is created in the asset directory. When using Portainer, that would be `/portainer/Files/AppData/Config/Homer/assets/config.yml`.
Section icons: https://fontawesome.com/v5/search
Application icons: https://github.com/walkxcode/dashboard-icons

## ShellInABox
SSH via the browser.
Accessed via port 4200 on HTTPS.

```sh
sudo apt install shellinabox
```

## Nginx Proxy Manager
To install, follow the instructions in the Portainer template.

## Nextcloud
```yaml
version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    image: yobasystems/alpine-mariadb:latest
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    restart: always
    volumes:
      - /mnt/hdd/nextcloud/mysql:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=rootpassword
      - MYSQL_PASSWORD=dbpassword
      - MYSQL_DATABASE=nextcloud_db
      - MYSQL_USER=nextcloud

  app:
    image: linuxserver/nextcloud:latest
    ports:
      - 8090:80
    links:
      - db
    volumes:
      - /mnt/hdd/nextcloud/html:/var/www/html
      - /mnt/hdd/nextcloud/conf.d:/usr/local/etc/php/conf.d
    restart: always

version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    image: yobasystems/alpine-mariadb:latest
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    restart: always
    volumes:
      - /portainer/Files/AppData/Config/nextcloud/mysql:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=rootpassword
      - MYSQL_PASSWORD=dbpassword
      - MYSQL_DATABASE=nextcloud_db
      - MYSQL_USER=nextcloud

  app:
    image: linuxserver/nextcloud:latest
    ports:
      - 8090:80
    links:
      - db
    volumes:
      - /portainer/Files/AppData/Config/nextcloud/html:/var/www/html
      - /portainer/Files/AppData/Config/nextcloud/conf.d:/usr/local/etc/php/conf.d
    restart: always
```
CREATE DATABASE nextcloud_db;
CREATE USER 'nextcloud'@'localhost' IDENTIFIED BY 'dbpassword';
GRANT ALL ON nextcloud_db .* TO 'nextcloud'@'localhost';
FLUSH PRIVILEGES;
EXIT;

## Pihole
On Raspberry Pi OS Bullseye, the Pihole docker may fail to start giving the following message:

```sh
Error response from daemon: driver failed programming external connectivity on endpoint pihole (...):
Error starting userland proxy: listen tcp4 0.0.0.0:53: bind: address already in use
Error: failed to start containers: 726d9b085815
```

To find which application is using port 53:

```sh
sudo netstat -antupl | grep :53
```
If it's `connmand` (the network manager) do the following.

Create `/etc/systemd/system/connman.service.d/disable_dns_proxy.conf`:

```sh
[Service]
ExecStart=
ExecStart=/usr/sbin/connmand -n --nodnsproxy
```

Then run:

```sh
sudo systemctl daemon-reload
sudo systemctl restart connman.service
```

This will disable the connmand DNS proxy.
Source: https://wiki.archlinux.org/title/ConnMan#Avoiding_conflicts_with_local_DNS_server

### WSL with Pihole
WSL can't find the DNS server when Pihole is used via Wireguard. Here is the solution.

Add the following to `/etc/wsl.conf` to prevent `/etc/resolv.conf` from being auto-generated (by default it points to `/mnt/wsl/resolv.conf`):

```sh
[network] 
generateResolvConf = false
```

Restart WSL from Powershell (admin):

```sh
wsl --shutdown
```

Now `/etc/resolv.etc` should be gone. Create it with the following contents specifying the main DNS server and a backup:

```sh
nameserver    x.x.x.x
nameserver    y.y.y.y
```

Restart WSL again and everything should work now.

___
## Dynamic DNS
In Google Domains:
- Select domain -> DNS -> Dynamic DNS -> Manage -> Create new record -> Enter subdomain.
- Click "View credentials" on the newly created record and copy the credentials.

Install ddclient on the Pi.

```sh
sudo apt install ddclient
```

ddclient config:
- Select "Web-based IP discovery service".
- 

dpkg-reconfigure ddclient
or
vim /etc/ddclient.conf

Option 1: googledomains native protocol

```sh
ssl=yes
protocol=googledomains
login='generated_username'
password='generated_password'
your_resource.your_domain.tld
```

Option 2: dyndns2 protocol

```sh
protocol=dyndns2
use=web
server=domains.google.com
ssl=yes
login='generated_usernam'
epassword='generated_password'
your_resource.your_domain.tld
```

For CloudFlare:
Create an API token with the permissions `Zone:DNS:Edit` and `Zone:DNS:Read`.
(https://medium.com/@timothy.halim/ddclient-cloudflare-setup-in-ubuntu-e271c53d3ce8)

```sh
ssl=yes
daemon=300
use=web
protocol=cloudflare
zone=domain.net
login=token
password='CloudflareAPIToken'
sub.domain.net
```

ddclient v. 3.9.1 doesn't support brearer auth from Cloudflare, so we need to patch it. Open `/usr/sbin/ddclient` and replace the lines

```sh
my $headers = “X-Auth-Email: $config{$key}{‘login’}\n”;
$headers .= “X-Auth-Key: $config{$key}{‘password’}\n”;
$headers .= “Content-Type: application/json”;
```

with

```sh
my $headers = "Content-Type: application/json\n";
if ($config{$key}{'login'} eq 'token') {
    $headers .= "Authorization: Bearer $config{$key}{'password'}";
} else {
    $headers .= "X-Auth-Email: $config{$key}{'login'}\n";
    $headers .= "X-Auth-Key: $config{$key}{'password'}";
}
```

Run ddclient manually to check that it works
```sh
# Clearing the cache first
sudo rm /var/cache/ddclient/ddclient.cache
sudo ddclient -daemon=0 -debug -verbose -noquiet
```

Restart the service

```sh
sudo service ddclient restart
```

Check sevice status

```sh
sudo service ddclient status
```

___
## Influxdb, Telegraf, Grafana
_NOTE!!! when setting up access tokens in Influxdb GUI use Ctrl-C to copy. "Copy to pasteboard" button does not work_

Grafana GUI:
- Use Flux as the query language
- URL: http://influxdb:8086
- Auth: all disabled
- Org and bucket: from Influxdb
- Token: generate one in Influxdb or use the user token

___
## Netdata
Automatically collect all kinds of useful device metrics (cpu, network, processes, etc.)

### Configure parent and child nodes
https://learn.netdata.cloud/docs/observability-centralization-points/metrics-centralization-points/configuring-metrics-centralization-points

___
## n8n Workflow Automation

_______________________________________________________________________________
# Using NTFS Disks
https://askubuntu.com/questions/11840/how-do-i-use-chmod-on-an-ntfs-or-fat32-partition/887502#887502

To allow setting permissions for NTFS disks, `ntfs-3g` is needed.

1. Install `ntfs-3g` from package manager.
2. Unmount the disk.
    ```sh
    sudo umount /mnt/hdd
    ```
3. Generate `UserMapping` file and place it on the disk after remounting.
    ```sh
    sudo ntfsusermap /dev/sda1
    sudo mount /dev/sda1 /mnt/hdd
    mkdir /mnt/hdd/.NTFS-3G
    mv UserMapping /mnt/hdd/.NTFS-3G
    ```
4. Update `fstab` (back up the old config).
    ```sh
    # nofail is very important as it allows the pi to still boot if the disk is not present
    UUID=34A0456DA04536A0 /mnt/windows ntfs-3g defaults,nofail 0 0
    ```
5. Unmount and try if the new setting works by mounting using `mount -a`.

_______________________________________________________________________________
# OS Specific
## Ubuntu Codename
```sh
lsb_release -cs
# In Ubuntu-based distros
cat /etc/os-release | grep UBUNTU
```

_______________________________________________________________________________
# Software

## Virtual Box
To enable clipboard:

```sh
sudo apt install virtualbox-guest-x11
# Run this and add it to .bashrc
sudo VBoxClient --clipboard
# Also set clipboard sharing in settings
```

## ROS2
Only LTS releases of Ubuntu are supported.

```sh
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
sudo apt update && sudo apt upgrade
sudo apt install ros-humble-desktop
sudo apt install ros-humble-xacro

# Update `.bashrc`
source /opt/ros/humble/setup.bash
```

Gazebo

```sh
sudo apt-get install lsb-release wget gnupg
sudo wget https://packages.osrfoundation.org/gazebo.gpg -O /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null
sudo apt-get update
sudo apt-get install ignition-fortress

sudo apt-get install ros-${ROS_DISTRO}-ros-gz
sudo apt-get install ros-$ROS_DISTRO-rviz
```

_______________________________________________________________________________
# Common Problems
Error: fatal error: openssl/opensslv.h: No such file or directory
  - Install openssl-devel:
    `sudo dnf install openssl-devel`
    libssl-dev for debian
