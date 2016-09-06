

### Raspberry Pi Home Setup

A history of how my two raspberry pi headless machines were set up at home.


#### Future

Consider writing a service to detect and deliver changes to raspberry PI IP addresses over a static location such as digitalocean/flask.

### Configuration

#### System

* Apt
    1. `sudo apt-get update`
    2. `sudo apt-get upgrade`
    3. `sudo apt-get install vim git tree tmux pwgen fail2ban`

* SSH Port
    1. Add additional ssh port `Port 2200` to `/etc/ssh/sshd_config`
    2. Restart ssh server: `sudo service sshd restart`
    3. Add ssh port forwarding on router

* Static IP: `sudo vim /etc/dhcpcd.conf`
    1. Append this to the file (change as necessary):
```
interface eth0    
static ip_address=192.168.1.111    
static routers=192.168.1.1    
static domain_name_servers=192.168.1.1 
```

#### raspi-config

* FIRST: Advanced Options -> Update (update the tool)
    - Note: if this triggers an update, this file will need updated too.

* Expand Filesystem (select it to auto expand)

* Change User Password: `pi` password to a `pwgen -cn 12` password

* Boot Options -> Console

* Internationalization
    1. Set timezone to `Pacific Ocean`
    2. Set keyboard to `101-key`, `US Standard`
    3. Set wifi country to `United States`

* Advanced Options
    1. Hostname -> Change to desired hostname
    2. Memory Split -> 16 (headless needs no gpu)
    3. SSH -> Enable (default)


#### User Management

* Add user
    1. `adduser robbintt` - use a new `pwgen -cn 12` password. Add robbintt to `sudo` group
    2. Create SSH keys `ssh-keygen`
    3. Add SSH pubkey to bitbucket dotfiles.git as deployment key
    4. `cd ~; git clone git@bitbucket.org:robbintt/dotfiles.git .dotfiles`
    5. Unpack dotfile symlinks w/ `make_symlinks.sh` script
    6. Log in as user, delete any `pi` account ssh keys.
    7. Configure dotfiles ssh to include user, port.
    8. Add authorized_keys from other machines as necessary and update .ssh/config in dotfiles. Redeploy dotfiles.

* Remove `pi` NOPASSWD sudo priveleges in `visudo`

