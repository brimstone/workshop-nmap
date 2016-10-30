Client To Server Communication
==============================

_Much more indepth answer at: https://github.com/alex/what-happens-when_

Let's start with a classic interview question: What happens when you type in
'google.com' in your browser and press the enter key.

Name Resolution
---------------

When your computer joined the network, it most likely used a protocol called
DHCP (Dynamic Host Configuration Protocol) to ask some machine on the network,
typically a router, for connection information. Typically this includes:

- IP Address lease
- Address of default gateway
- Address of nameserver

The computer joining the network broadcasts a UDP packet, using the DHCP format,
with its hostname, and MAC address.

Connect to IP Address
---------------------


HTTP Request
------------


