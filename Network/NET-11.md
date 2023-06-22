# Access Control List

## Table of Contents
1. ACL Overview
2. Standard ACL Implementation
3. Extended ACL Implementation
4. Review from Quizziz
# ACL Overview

## Concept: Access Control List

* Where its used in, 
1. computer networks (firewalls, switches, and routers)
2. Computer File Systems ( Servers and workstations )
3. Web portals ( Canvas, amazon )
4. Cloud configurations ( Amazon web service VPC, microsuft Azure VNET)

## ACL Definition: Computer Networks

* ACL ( Access Control List) is a rule-based feature that allows network administrators and engineers to configure basic traffic filtering.
* ACL is a series of commands that, based on information in the packet header, determine whether to drop a packet or forward it.
* This is working w/ routers to filter traffic and not firewalls. its like a lightweight firewall ability, it is limited but better than nothing

## Stateless vs. Stateful

* One device that contains ACLs are firewalls.
* Stateless firewalls will look at source and destination w/ conditions that allow or block traffic. it doesnt know the difference between good/bad traffic its only knows whats configured manually, it only looks at the header/frame it doesnt look at the actual data coming through, very basic and simple.this is old technology, a legacy firewall
* Stateful firewalls will understand the details of a connection and allow the return traffic. 
* NGFW , next generation firewalls, advancement from stateful firewalls, a stateful is a physical and it uses ports,protocols, ip addresses, and the ngfw examines that actual info in the packets

## ACL Advantages

* **Advantages of configuring an Access List on a device.**

1. Network Performance: Network performance can be improved by allowing only relevant services to c ommunicate w/ devices across the network.
* For Ex. restricting the network to block video traffic can improve network performance.
2. Securing the Network: In a network environment, users may be restricted from accessing sensitive services.
* ACL provides a basic level of network security by allowing some hosts to access parts of the network, while preventing others from accessing the same parts.

## Additional ACL Capabilities

* **Protocol Restriction**
* ACLs can also restrict the following
* Routing protocol advertisement messages
* Packets from security protocols
* Packets from other protocols, such as ICMP

* We would block ICMP because we don't want people pinging our network, its for diagnostics, but it actually does have payload still and hackers could transfer data explotation through ICMP, theres a thing called the ping of death. we block segments of our network that are facing the internet to prevent any sort of explotation.

## Standard vs. Extended

* **There are standard ACLs and extended ACLs, w/ the difference in the parameters examined in the process.**

* Standard ACLs: Standard acls examine only the source ip address, they only filter info from source ip address, when implenementing restrictions, Cisco recommends to place this type of ACL as close to the destination device as possible.
* Extended ACLs: Extended ACLs filter packets according to the following parameters: protocol type, source or destination IP address, and source or destiniation port. Cisco recommends to place this type of ACL as close to the source as possible.

## Traffic Direction
* **When configuring ACL, traffic direction, inbound or outbound, must be specified on an interface. This is done so that router will implement the proper restrictions when examining the source network and destination.**

* **Inbound ACL**: Configuring the ACL for inbound traffic, the router will examine incoming traffic to the interface.-------->

* **Outbound ACL**: Configures the ACL for outbound traffic, the router will examine outgoing traffic from the interface. <------

## Wildcards
* Wildcards, are inverted subnet masks that can be used in statements in both extended and standard ACLs
* For ex. 255.255.255.0 
* Binary equivalent = 1111111.1111111.1111111.0000000
* inverts to a wildcard mask of 0.0.0.255
* binary equivalent - 0x8.0x8.0x8.11111111

## ACL Order
* **The order of statements in an ACL is CRUICAL**

* **Check Order**: **ACEs**( Access Control Entries), which represent the order of statements in the ACL, are crucial and must be carefully planned. The router checks each packets parameters against the ACEs to find a matching condition. When a condition is met, the ACL will be applied, and additonal ACEs will be ignored.

* **Implicit Deny**: At the end of every ACL, there is an invisible statement called implicit deny. When no match is found for a packet, the implicit deny is applied to the packet. **Each ACL Must have atleast one permit statement**

# Standard ACL Implementation

* Where are Standard ACLs placed? Standard ACLs are placed as close to the destination as possible.
* Cisco set this rule because placing standard ACLs at the source of traffic will prevenet communication w/ any network hosting interfaces to which the ACL applies.,
* **standard ACLs filter traffic only according to the source IP address.**

## Named vs. Numbered
* **ACLs can be assigned unique names or numbers**

* **Standard Named ACL**: Standard Named access control list allow unique names to be assigned to ACLs.

* **Standard Numbered ACL**: Standard numbered accesss control list allow unique numbers to be assigned to ACLs.
* The standard numbered ACL range includes 1-99 and 1300-1999.

## Standard Numbered ACLs

1. COMMAND: access-list < access-list-number >
< deny|permit|remark > < Source-address> < source wildcard >

1. R1(config)# access-list 10 permit 192.168.10.0 0.0.0.255

1. beginning syntax to configure a numbered ACL
2. Decimal number from 1 to 99 or 1300 to 1999 (only! for Standard ACLs)
3. Deny denies access if the conditions match, permit permits access if the conditions match, and remark adds a remark about entries.
4. IP of the network or host from which the packets were sent, you can specify any instead of using a 32-bit address.
5. 32-bit wildcard mask that will be applied on the source.

## Standard ACL Scenario

![Alt text](<assets/Standard ACL Scenario.PNG>)
![Alt text](<assets/Scenario 1.png>)
we can have an ACL only in 1 direction, so 1 inbound and 1 outbound

## Standard Number ACL Config Ex

1. R1(config)#access-list 1 deny 10.0.0.0 0.0.0.255
2. R1(config)#access-list 1 permit any
3. R1(config)# int g0/3
4. R1(config-if)#ip access-group 1 out
5. R1(config-if)#exit

1. Step 1, create a numbered ACL using the access-list command
2. step 2, choose the interface for which the acl will apply, using interface command
3. step 3, ip access0group 1 out command links ACL 1 to the g 0/3 int in the outbound direction.

## Standard Named ACL config Ex

1. R1(config)# ip access-list standard BLOCK__HOST_A
2. R1(config-std-nacl)#deny host 192.168.0.10
3. R1(config-std-nacl)#permit any
4. R1(config-std-nacl)#exit
5. R1(config)#int g0/2
6. R1(config-if)#ip access-group BLOCK__HOST_A
7. R1(config-if)#exit

1. Step 1 - use the ip access-list standard command to create a named ACL
2. Step 2 - IN ACL configuration mode, create Deny and Permit ACE statement
3. Step 3 - Apply the ACL on an int using ip access-group command, and specify the traffic direction ( in or out)

## Verify ACL Settings

![Alt text](<assets/Verify ACL Settings.PNG>)

# Extended ACL Implementation

* Extended ACLs filter packets based on the following attributes:
* source and destination IP addresses
* Source and destination layer4 protocols (UDP and TCP)
* Protocol type or number, for ex. IP, HTTPS, 80, etc.
* Extended ACLs use the following range of numbers : 100 to 199 and 2000 to 2699.

## Extended ACL Placement

* Configure Extended ACLs as close to possible to the source of the traffic being filtered.
* Doing so ensures that traffic will be denied and prevented from traversing the network infrastructure.

* **Its important to understand that even if the ACL is not placed as close as possible to the source, the ACL will still operate as it should.**

## Extended Numbered ACLs

1. COMMAND: 1 access-list <2  number > < 3 action > < 4 protocol > < 5 source-address> < destiniation-address > < 6 operator >
1. R1(config)#access-list 101 deny ip host 10.0.0.1 host 172.16.0.2
2. R1(config)#access-list 101 deny tcp host 10.0.0.2 host 172.16.0.3 eq 22

1. Syntax used to configure #'d ACL
2. Decimal numbers, extended ACLs use 100-199 and 2000-2699
3. deny denies access if the conditions match, permit permits access if the conditions match, and remark adds a remark about entries.
4. the name of the protocol being used: IP, TCP, UDP, ICMP, etc.
5. the source and destination of the network traffic, which can be host, or a network 32-bit address. the any option can be used, and different combinations can also be used.
6. for logical port configuration, the following operators can be used for more control: it(less than), gt(greater than), eq( equal to), neq( not equal to), and range (inclusive range)

* When we type ip in our commandline , this means all traffic, access-list 100 [ ip ] 192 to 10 it means all traffic, all data, all packets denied
![Alt text](<assets/Extended Acl Examples.png>)

* Scenario 2, out FTP Server runs on ports TCP 20/21 so we have to block out port 20/21 

* we do permit any any; this is any [ source ] any [ destination ] 


# Review from quizziz
Which method is used for in-band management of a cisco device? remember in-band means inside the network the logical side, the software side, this isnt hardware, ssh is software secure shell, we could use telnet but its not secured, it will be displayed as plain text, this is why we use ssh or secure telnet.

Standard ACLs permit or deny traffic according to destination address, this is false because it can only allow traffic that is named for it, **it only denys or permits traffic based on source.**
RIPv2 does support CIDR(Classless inter-domain routing ) and VLSM (variable length subnet mask )

Binary number system uses a 2 base system.

port security violation modes are, protect, restrict and shutdown

router store the routes used in forwarding decisions in the routing table

device used to separate collision domains is a switch

an ARP request is sent as a broadcast, ARP is address resolution protocol, used for discovering the link layer address such as a mac address aka physical address, associated w/ a given internet layer addressed like an IPv4, its for connecting ip addresses to mac addresses

Physical addressed stored in a cisco device will be found in the MAC address table

the first mode we are in when accessing a cisco cli is called the user exec

another name for a NAT (network address translation)  overload also known as PAT, ( port address translation)  is designed to map multiple private ip addresses to a single Ip address many-to-one by using different ports

FCS is used to verify the integrity of a frame, FCS is called a frame check sequence.

Extended ACLs can filter data using their source and destination address and source and destination port

the command we use to display status of all interfaces on a cisco switch is show interfaces status

main advantage of TCP is its reliability

A DHCP is used to assign IP addresses to hosts, aka endpoints

The TCP/IP model contains 4 layers

Administrative distance specify for a routes reliabilty 

where should you place a standard acl, we place those as close to the destination

The native VLAN is used to forward untagged traffic, which is true. VLAN1 is the native default vlan and it does not need to be configured, we would want to change it to anything else, so we want to change it from vlan1 so that any hacker will not be able to hop inbetween all the other vlans, we have to make sure that the native vlan is matched, we have to tag them. 
