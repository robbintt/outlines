### Procedure: Set up ssh as a SOCKS proxy over 443

"A simple VPN." - lee


#### Prerequisites

The remote server's sshd needs to accept ssh on 443 if you can only get 443 outbound.

Edit `/etc/ssh/sshd_config` to have the line `Port 443` after any similar lines and `service sshd restart`


#### Server and client setup

1. `ssh -p443 -D localhost:443 <username>@<remote-host>`
    - macos: `sudo ssh -i <path-to-ssh-key> -D localhost:443 <username>@<remote-host>`
        - make sure to use the path to the private key, not the public key!!
2. Configure your local system to send network traffic over a SOCKS proxy at localhost:443
    - macos: `System Preferences->Network`
        1. unlock administrative access (press the lock)
        2. select 'wifi' for wifi 
        3. choose `Advanced...->Proxies`
        4. Add `localhost` : `443` to the `SOCKS Proxy`, choose `ok`
        5. In the 'network' window choose `save`
        6. Check your IP at [google.com](google.com) by typing "whats my IP"


