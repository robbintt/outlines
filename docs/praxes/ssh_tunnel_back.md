
### Setting up tunneling back into an SSH connection

This is for establishing a new connection back to the server through the original SSH connection.

This is typically used if you are behind a proxy but the machine you want to be on is not.  You can access the machine, then use that tunnel to access your machine.

The best use case for this is if you have some non-ssh access to a remote machine and need to establish a tunnel back to your local machine in order to have direct ssh access to the remote machine.

One use case for this might be a citrix desktop.


### Definitions

This gets confusing so we will use 2 terms to disambiguate each server.

1. `Establishing Server` - The server which sends the first SSH connection. Its SSH connection will be tunneled back through.
2. `Remote Server` - The server that receives the original SSH connection and is used to tunnel back into the `Establishing Server`


### Setup

1. Open `/etc/ssh/sshd_config` and add the line `GatewayPorts yes`
2. Create a tunnleable connection from the `Establishing Server` to the `Remote Server`.
    - `ssh -R 2000:localhost:22 yourusername@remoteservername -p22`
3. Tunnel back from the `Remote Server` to the `Establishing Server`
    - `ssh -p2000 yourusername@localhost`
4. This connection is only available through loopback/localhost


### References

- [ServerFault 'SSH back to local machine from remote SSH session'](http://serverfault.com/questions/175798/ssh-back-to-the-local-machine-from-a-remote-ssh-session)
- [AskUbuntu reverse port tunneling](http://askubuntu.com/questions/50064/reverse-port-tunnelling)
- `man sshd_config`
