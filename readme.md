Build Firewall
==============
This script builds a firewall with a default DROP policy.

Optimised for Ubuntu (16.04) server.

All IPv6 traffic is dropped.

## Installation & Usage
1. Clone this repo (e.g. to `~/sysadmin`)
2. Enter the local IP address (`$HOME_IP`) (to lock down pinging) in the `build-firewall` script
3. Enter the `SSH_PORT` in the `build-firewall` script
2. Make `build-firewall` executable
2. Create a symlink to `build-firewall` from within your `$PATH`
3. Run as `build-firewall` as sudo

~~~sh
cd ~/sysadmin/firewall
sudo chmod +x build-firewall
ln -s ~/sysadmin/firewall/build-firewall /usr/local/sbin/build-firewall
~~~

## Persistence
Note that firewall rules are held in memory - they won't persist across reboots.

Use `iptables-persistent` to load rules on boot.

**Important**: if you change rules, run `sudo dpkg-reconfigure iptables-persistent`.

## Resources
- Iptables Man Page: https://linux.die.net/man/8/iptables
- Comprehensive set of rules, well commented: http://www.thegeekstuff.com/scripts/iptables-rules
- As above: https://crm.vpscheap.net/knowledgebase.php?action=displayarticle&id=29
- OUTPUT rules, implications for security: http://serverfault.com/a/433304
- Persistence! http://dev-notes.eu/2016/08/persistent-iptables-rules-in-ubuntu-16-04-xenial-xerus/
- More examples of rules: http://www.thegeekstuff.com/2011/06/iptables-rules-examples/
- Linode guide to server security: https://www.linode.com/docs/security/securing-your-server#basic-iptables-rulesets-for-ipv4-and-ipv6
- Listing, deleting rulkes: https://www.digitalocean.com/community/tutorials/how-to-list-and-delete-iptables-firewall-rules
