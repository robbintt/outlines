## VNC Reverse Proxy

In order to create a reverse proxy, you will need access to the server behind the firewall and a computer with a static IP address to proxy/receive the connection from your laptop.

### Steps

1. Setup - proxy server/computer
    - Make sure it has a static IP and that the sshd server is active
    - Set the `sshd_config`'s `GatewayPorts clientspecified` - this is used to allow any domain to hit the proxy
2. Installation - computer/server behind the firewall
    - `apt install autossh tightvncserver xfce4 xfce4-goodies firefox`
    - store the vnc server password somewhere safe, choose `connection 1` as that corresponds to `port 5901`
    - Write a systemd unit for connecting to the proxy
    - replace `your_username_here` with your username and `1.2.3.4` with the IP or DNS hostname of your proxy server
    - Install the systemd service, restart the `daemon`, `start` it, and `enable` it.


```[Unit]
Description=AutoSSH Tunnel
After=network.target

[Service]
User=your_username_here
Environment="AUTOSSH_GATETIME=0"
ExecStart=/usr/bin/autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -NR *:5901:localhost:5901 your_username_here@1.2.3.4 -p 22

[Install]
WantedBy=multi-user.target
```


3. Connect to vnc server
    - use the default mac client `$ open vnc://1.2.3.4:5901`
    - you should not need to specify a username or anything else
    - or use a specialized client


### Future

1. Configure the `tightvncserver` service or pick a different one if preferred.
2. Consider better macos, windows, linux vnc clients and special configuration options
3. Option: per-user vnc connection instead of per user proxy

