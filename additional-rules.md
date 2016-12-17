Additional Rules
================
Additional & oiptional rules here, to keep main script clean:

~~~sh
# Allow outgoing SSH: Connect from this server to an outside server
$IPT -A OUTPUT -o eth0 -p tcp --dport $SSH_PORT -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A INPUT -i eth0 -p tcp --sport $SSH_PORT -m state --state ESTABLISHED -j ACCEPT

# Allow outgoing SSH only to a specific network DO WE NEED THIS???
$IPT -A OUTPUT -o eth0 -p tcp -d 192.168.101.0/24 --dport $SSH_PORT -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A INPUT -i eth0 -p tcp --sport $SSH_PORT -m state --state ESTABLISHED -j ACCEPT

# Allow packets from internal network to reach external network.
# if eth1 is connected to external network (internet)
# if eth0 is connected to internal network (192.168.1.x)
$IPT -A FORWARD -i eth0 -o eth1 -j ACCEPT

# Allow incoming HTTPS, with output allowed on an established connection
$IPT -A INPUT -i eth0 -p tcp --dport 443 -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A OUTPUT -o eth0 -p tcp --sport 443 -m state --state ESTABLISHED -j ACCEPT

# Allow outgoing HTTPS: helpful when using wget to install files etc.
$IPT -A OUTPUT -o eth0 -p tcp --dport 443 -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A INPUT -i eth0 -p tcp --sport 443 -m state --state ESTABLISHED -j ACCEPT

# Original rule/settings for prevention of DoS attack
iptables -A INPUT -p tcp --dport 80 -m limit --limit 25/minute --limit-burst 100 -j ACCEPT

~~~
