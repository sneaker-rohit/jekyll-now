**Dynamic Host Configuration Protocol** is a client/server protocol that is used for automatic allocation of IP addresses to the clients on the network. It maintains a pool of IP addresses and leases out the addresses when a DHCP enabled client asks for it. DHCP makes use of the UDP protocol and works on port 67 (server) and port 68 (client). The DHCP handshake has 4 messages.

1. DHCP DISCOVER - DHCP client sends out a broadcast message asking for an IP address.

2. DHCP OFFER - the DHCP server that listens to the DISCOVER message from the client, offers the list of IP available to the client.

3. DHCP REQUEST - the DHCP client agrees to the offered IP addresses from the DHCP Server and sends out a DHCP REQUEST to confirm.

4. DHCP ACK - the DHCP Server makes a note of the MAC of the client and the IP it has allocated to it. It then, sends across a DHCP ACK to the client along with the lease time for which the IP is valid.

A good technique to remember the handshake would be to remember the name DORA.

Usually, every network has a DHCP server setup. However, it is also possible that the DHCP server might  be in a completely different subnet and in such cases we make use of the DHCP relay agent. The relay agent receives the request from the client and forwards it across to the DHCP server. It acts as a middleman and helps the client obtain an IP address.

The DHCP-client usually with Option 50 set can request for a specific IP address every time to the DHCP server. Obtaining a same IP every time can help with network settings and troubleshooting.


Troubleshooting DHCP - the best way to learn more about DHCP and what's going on under the hood is to launch Wireshark and look at the packet capture. The capture filter that could be used to look at the DHCP messages is `bootp`. Enter the filer and inspect through the messages.

Common Issues with DHCP - Server does not respond or it responds with an incorrect IP address. Moreover, one possibility could be the presence of a Rouge DHCP server on the network which is perhaps doing all the malicious stuff.



