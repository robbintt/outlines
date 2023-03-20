### `lftp` FTPS/FTP Automation

We want to use `ftps` which uses FTP over TLS/SSL. This is not the same as `sftp` which is FTP over SSH.

- FTP Server: <server>
- Port: 990
- User name: <user>
- Password: <pass>

The user name does not allow @. This may be possible somehow.


### Example with `lftp` command line FTP/FTPS program

#### FTPS Example

Note that you must specify ftps:// in the URL.

`lftp -c "open -p990 -u <user>,<pass> ftps://<FTP Server>; ls"`


#### FTP Example

`$ lftp -c "open -u <user>,<pass> <FTP Server>; ls"`

This can be used to send and receive files automatically via scripted action.


#### Security

Always use FTPS over port 990.

Standard (Port 21) or Implicit SSL/TLS (Port 990) are available. 

