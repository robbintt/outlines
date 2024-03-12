# SSH Port Forwarding

This covers a simple example.

Permutations of `-L` can be read in the ssh manpage.

`ssh -L local_socket:host:host_port`


## Example

This can be used to establish a connection to jellyfin on a remotehost on `localhost:8000`

`ssh -L 8000:localhost:8096 -p 22 -i ~/.ssh/id_rsa user@remotehost`
