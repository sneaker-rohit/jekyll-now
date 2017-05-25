Source Routing is a feature that allows the sender of the packet to specify the route that the destination must take while sending back an reply. Now, assume a situation that an attacker manages to inject a source routed packet into your network. The attacker might configure a malicious path for the packet and cause security issues.

It is best to disable source rotuing. On Cisco routers, the source routing can be disabled by

configure terminal 
no ip-source 

On Linux based machines, one of the method to disable the source rotuing is by editing the configurations.
Execute the below code and restart the networking services (/etc/init.d/networking restart) for the changes to take effect.

`for f in /proc/sys/net/ipv4/conf/*/accept_source_route; do`
    `echo 0 > $f`
`done` 