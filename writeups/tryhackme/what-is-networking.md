What is Networking? — TryHackMe

Platform: TryHackMe
Room: What is Networking?
Date Completed: June 5, 2026
Flags: THM{YOU_GOT_ON_TRYHACKME} | THM{I_PINGED_THE_SERVER}
Medium Article: Read here


What is a Network?
When technological devices are connected together to communicate based on rules — that connection is called networking.

The Internet
The Internet is a giant network made up of many smaller networks
First iteration: ARPANET project in the late 1960s
World Wide Web created by Tim Berners-Lee
Small networks = private networks
Networks connecting small networks = public networks (Internet)


Identifying Devices on a Network
Every device has two means of identification:
1. IP Address (Internet Protocol)

Set of numbers divided into four octets (e.g. 192.168.1.1)
Each octet ranges from 0–255
Calculated through IP addressing & subnetting
Can change from device to device
Cannot be active simultaneously more than once on the same network
IPv4 uses 2^32 addresses = ~4.29 billion (hence the shortage)
IPv6 introduced to solve shortage (e.g. 2a00:22c4:a531:c500:425f:cce6:c36b:f64d)
Public IPs assigned by ISP
Devices on same network share one public IP

2. MAC Address (Media Access Control)

Physical address assigned at factory — burned into the network interface card
12-character hexadecimal number (e.g. a4:c3:f0:85:ac:2d)
First 6 characters = vendor who built the interface (e.g. Intel)
Last 6 characters = unique address of that interface
Can be spoofed — attacker fakes MAC to bypass firewall rules

MAC Spoofing Attack Example:
If a firewall only allows traffic from the admin's MAC address,
an attacker can spoof that MAC and the firewall will treat them as the admin.
Practical: Spoofed MAC address on free hostel WiFi simulation → got flag THM{YOU_GOT_ON_TRYHACKME}

Ping (ICMP)

Most fundamental network diagnostic tool
Uses ICMP (Internet Control Message Protocol) packets
Measures performance/connectivity between devices
Syntax: ping <IP address or URL>

Practical Task — Ping Google DNS
bashping -c 4 8.8.8.8
Output:
PING 8.8.8.8 56(84) bytes of data
64 bytes from 8.8.8.8: icmp_seq=1 ttl=56 time=7.32 ms
64 bytes from 8.8.8.8: icmp_seq=1 ttl=56 time=9.69 ms
64 bytes from 8.8.8.8: icmp_seq=1 ttl=56 time=9.40 ms
64 bytes from 8.8.8.8: icmp_seq=1 ttl=56 time=9.77 ms
4 packets transmitted, 4 received, 0% packet loss
Flag: THM{I_PINGED_THE_SERVER}

Key Takeaways

The Internet = network of networks (private + public)
Every device has an IP (logical, changeable) and MAC (physical, permanent)
IPv4 shortage is real — IPv6 was created to solve it
MAC addresses can be spoofed — firewalls relying only on MAC are vulnerable
Ping uses ICMP and is the first tool to check connectivity
Understanding networking is the foundation of both offensive and defensive security

