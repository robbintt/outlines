## Noisebridge infosec meetup 2017.08.31

Organizer: Kelly Albrink
Topic: Kiopatrix 3 (kiopatrix 1.2)


### VirtualBox

I installed `vmware` but I used `VirtualBox` because I am more familiar with it.


### Network: `NatNetwork`

In `virtualbox->preferences->network` I added a new NatNetwork called `PartyTime`.

I attached both the `attacker` and `kiopatrix1.2` virtual machines to the `PartyTime` network.

Both attacker and defender must be on the same VirtualBox `NatNetwork`.  You can change this for machine in its `settings->network`.


#### Getting internet connectivity

After setting up the host-only network, the route might be messed up in the attacker machine.  You have to fix your routing:

- Run:
    - `dhclient eth0`

#### Get ssh server up on attacker

So I can use my native terminal.

- https://lmgsecurity.com/blog/enable-start-ssh-kali-linux/
- 

### Attacker VM

The VM can be ssh'd into from the host. It's got a DHCP IP on 192.168.56.0/24.

#### Setting up the attacker vm for native terminal (no virtualbox window)

1. Install sshd and set it up.
2. Make sure root can login with a password
3. From host: `ssh root@192.168.1.<D>`
    - you should just have to accept the host key and give the password: `toor`

I set up kali linux light `.ova` file as my attacker machine. It seems to work just like an `ovm` machine (you import it as an appliance in VirtualBox.

- username: root
- password: toor


### Defender VM

I set up the Kiopatrix vmdk file as my defender by making a new vm and adding the VMDK as the attached drive. I specified ubuntu but it didn't seem to take that setting. I assume I could have set anything and it would just use the VMDK and do nothing. Weird.

Kiopatrix says: set up your /etc/hosts in your attacker VM:

```<kiopatrix ip> kioptrix3.com```


### Resources

1. [Kali Linux VMs](https://www.offensive-security.com/kali-linux-vmware-virtualbox-image-download/)
1. [kiopatrix 3](https://www.vulnhub.com/entry/kioptrix-level-12-3,24/)
