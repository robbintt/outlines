### Managing traffic: `iptables` and `ip6tables`

`iptables` is used to manage IPv4. `ip6tables` is used to manage IPv6.


#### Using `iptables` rules

Ubuntu recommends using `ufw` to easily manage `iptables rules`.

1. View current rules: `iptables -L`
2. Rules are applied in order
    - One a rule `ACCEPT`s or `DROP`s a packet, no further rules are applied
3. Three `chain`s: `INPUT`, `FORWARD`, `OUTPUT`


#### Saving & Restoring iptables rules

1. `iptables-save` dumps the current iptables to stdout.
2. `iptables-restore` flushes iptables and restores a `iptables-save` dump.
3. Procedure
    1. When your `iptables` is correct, run as root: `$ iptables-save > dump.iptables`
    2. To flush `iptables` and reload, run as root: `$ iptables-restore < dump.iptables`
4. There are additional options to maintain packet/byte counters, skip flushing, or save only one table by name.


#### Permanently modifying iptables in a debian/ubuntu system

By default, iptables is only stored in memory. Management tools exist for iptables including `ufw` and the `iptables` service.

1. `iptables` initial ruleset comes from `/etc/network/interfaces` (may be `/etc/sysconfig/iptables`)
2. 


#### Resources

1. [help.ubuntu.com IptablesHowTo](https://help.ubuntu.com/community/IptablesHowTo)
2. [nixCraft: How Do I Save Iptables Rules and Settings?](https://www.cyberciti.biz/faq/how-do-i-save-iptables-rules-or-settings/)
3. [askubuntu managing iptables with ip6tables](http://askubuntu.com/questions/398672/do-i-also-need-to-set-up-another-iptables-rules-for-ipv6-if-i-just-used-iptables)
4. manpages: `iptables`, `iptables-save`, `iptables-restore`
