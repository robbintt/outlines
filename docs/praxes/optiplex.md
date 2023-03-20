## Setting up a Dell OptiPlex FX160

1. Use a sata 22-pin extender to add a 2.5" drive
1. Update the `BIOS Settings`
    1. In `System` -> `Boot Options` (make sure both the drive and usb are inserted)
        1. `Hard Drive`
        1. `USB`
        1. (no option)
        1. (no option)
        1. (no option)

    1. In `Drives` -> `SATA Operation` select `AHCI`
    1. Optional: reset security settings by unseating the bios coin battery for 1 minute
1. Download `xubuntu 16.04.2 iso` and write to a `flash drive`
1. Attach a monitor, keyboard, mouse, and ethernet cable or USB wifi card
1. `install xubuntu`
    - Select: `install 3rd party software` and `download updates during install`
    - Set an appropriate: `hostname`, `username`, and `password`
    - Install `vim`, `openssh-server`, and `openssh-client`
1. Get a static IP on your local network (lan)
    - Paste the contents in the snippet below into `/etc/network/interfaces`

	```
	# interfaces(5) file used by ifup(8) and ifdown(8)
	
	# default loopback interface (from install)
	auto lo
	iface lo inet loopback
	
	auto enp2s0
	iface enp2s0 inet static
	address 192.168.1.ddd
	netmask 255.255.255.0
	gateway 192.168.1.1
	
	# google DNS
	dns-nameservers 8.8.8.8
	```

    - Update your `address` and `gateway` for your local network
    - Additionally, your interface name may be different, here called `enp2s0`
        - Find your interface by typing `ifconfig`, it is the one that is not `lo`
        - Make sure you are setting up the interface you will always be using
    - Ubuntu guarantees consistent naming for these interfaces per hardware configuration
1. SSH into your computer through your local network at the correct local IP 
    - If you will connect over the internet, test this too through a remote connection
1. Restart the computer, optionally test SSH again
1. If everything works, you can remove the peripherals and manage the machine through SSH
1. This guide does not cover securing or managing your installation.


