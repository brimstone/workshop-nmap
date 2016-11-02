Identification
==============

There's a couple of different ways to determine the IP address of a system. The
simplest maybe is using the command `ifconfig` or `sudo ifconfig` on Linux, or
`ipconfig` in Windows.


`ifconfig` output on Linux:

```
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 0  bytes 0 (0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.100  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::fa16:54ff:fe4f:ccc5  prefixlen 64  scopeid 0x20<link>
        ether de:ad:be:ef:ca:fe  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

`ipconfig` output on Windows:
```
Microsoft Windows [Version 6.3.9600]
(c) 2013 Microsoft Corporation. All rights reserved.

Windows IP Configuration

   Host Name . . . . . . . . . . . . :
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : hsd1.ut.comcast.net.

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : hsd1.ut.comcast.net.
   Description . . . . . . . . . . . : Qualcomm Atheros AR8171/8175 PCI-E Gigabit Ethernet Controller (NDIS 6.30)
   Physical Address. . . . . . . . . : 00-26-18-AC-EF-7D
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::4516:c43a:e475:9a86%12(Preferred)
   IPv4 Address. . . . . . . . . . . : 192.168.0.100(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . . : Wednesday, October 06, 2010 8:14:50 PM
   Lease Expires . . . . . . . . . . : Wednesday, October 06, 2010 8:19:49 PM
   Default Gateway . . . . . . . . . : 94.202.195.1
   DHCP Server . . . . . . . . . . . : 94.202.195.1
   DHCPv6 IAID . . . . . . . . . . . : 285222424
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-12-A7-92-DC-00-26-18-AC-EF-7D
   DNS Servers . . . . . . . . . . . : 75.75.75.75
                                       75.75.76.76
                                       192.168.1.1
   NetBIOS over Tcpip. . . . . . . . : Enabled
```

The main thing used in this lab is the `inet 192.168.0.100 netmask 255.255.255.0`
line. This is the IP address of both systems used in the example. The netmask
portion is used by the Operating System to know which IPs are local to this
system, and which need to be directed to the default gateway.

CIDR (Classless Inter-Domain Routing) Notation
----------------------------------------------
_Much, much, better info at https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing_

There's a whole bunch of information here about the notation and how to convert
to and from CIDR notation. The main thing we need to know here is the following:

- 192.168.0.100/255.255.255.0 => 192.168.0.0/24

nmap supports CIDR notation and also ranges. The following range could also be
used as input to nmap:

- 192.168.0.100/255.255.255.0 => 192.168.0.1-254


Your first scan
---------------

How to scan the network with nmap

`nmap -sP 192.168.0.1-254`

How to scan all of the ports on a system with nmap

`nmap $target`

Results
```
Starting Nmap 7.31 ( https://nmap.org ) at 2016-11-01 20:19 EDT
Nmap scan report for target (192.168.0.101)
Host is up (0.0011s latency).
Not shown: 997 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
1024/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 4.65 seconds
```

By default, nmap uses a "Connect Scan" where it sends SYN packets, waits for the
ACK, then ACKs back, and opens a session. nmap immediately closes the session.
