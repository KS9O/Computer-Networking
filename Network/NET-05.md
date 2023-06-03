# IP & Routing Concepts

## Table of Contents
1. Decimal, Binary & Hex
2. The Router, itself
3. Routing Process
4. IPv4
5. IPv6
# Decimal, Binary, & Hex
## Decimal Numbering System
* Base 10 = 1- digits
* 0-9
* We have place values, where its from left to right
* theres the 1's place, then we have the 10's place, and then the 100's, it place value is a power of 10, 1's place is 10 squared 0, 10's place is 10 squared 1, 100's place is 10 squared 2, then the 1000's place, which is 10 cubed 3.

Anything of the 0 power = 1
## Binary Number System
on and off are 2 values, transitters do this 
* Base 2, numbering system, = 0, 1
* Binary has place values of 2 by the power of 2
1. 2 to the power of 0 = 1's place ( these are the decimals numbering)
2. 2 to the power of 1 = 2's place [ decimal # ]
3. 2 to the power of 2 = 4's place [ decimal # ]
4. 2 to the power of 3 = 8's place [ decimal # ]
5. and so on, we would contiune to add 2 to the power of 4, 5 , 6
* we usually take binary into a decimal number to make it easier to understand, which is exactly what we do w/ IP addresses, we convert the binary into the decimal and thats how we get an IP.
![Alt text](assets/Binary%20Numbering%20System.PNG)

## Hexademical Numbering System
* Base 16 numbering system, has 16 numbers
* 0-9 , nothing bigger than a 9 is represented for value, we use letters, 
* A = 10
* B = 11
* C = 12
* D = 13
* E = 14
* F = 15
![Alt text](assets/Hexadecimal%20Number%20System.PNG)

* We can to compress this binary number and convert it to a hexadecimal, which would make our binary, 1 1 1 1 , go into our decimal numbering system of 15, which converting it into hexadecimal converts it to 15.

we take it into 4 bits into a nimble

https://app.whiteboard.microsoft.com/me/whiteboards/9a3ec608-5a2f-4a0a-81d5-125e7f2e8a9b

# The Router

* Router is a layer 3 OSI layer, it forwards traffic based on IP addresses.

* **Router**: A router is a devince designed to receive, forward, and analyze packets transmitted to and from other devices on a network and other networks. Routers enable inter-network communication and can provide services such ACL and NAT, which are required in any networking scheme.
* **A router is a lyer 3 device that communicates using IP addresses**

## Default Gateway
* This is our exti door.

* **Default Gateway**: The default gateway is a network device that can route traffic to and from other networks, a router typically fulfills this role.
* The default gateway is similar to the door of a room, if a desired object is in another oom, the object can be reached only by exiting through this door.
* **If the destination is on the same network, there is no neede to pass throug the router.**
* It is allocated either manually or through DHCP, we configure the gateway.

**Default Gateway Configuration**: typically located together with other adpater configuration options. It is in our IPv4 properities.

* by default, the gateway should be received from the DHCP, but if the manual IP's are configured, the gateway should also be configured manually.

* We assign a computer an IP address, and the gateway address is the way the data leaves out.

## Router Interfaces

* **Fast ethernet interface**: Fast ethernet was first made public in 1995, ethernet operates at a speed of 100mbps and uses the media standard 100baset.
* **Gigabit Ethernet Interface**: Gigabit etherent was introduced in 199, it supports a faster speed of 1,000mbps and uses the meida standard 1000baset but can also support 100mbps.
* **Serial Interface**: Serial interfaces are used for long-distance transmissions, its usually for ISP's, if two sedrial ports need to communicate w/ each other, they must be syncronized w/ the same clock frequency and allocate the necessary bandwitch.

## Interface Configuration
* Router interfaces must be set up w/ IP addresses, similar to computer network interfaces.
* the Interface [type] [id] command selects the desiered interface, to use an interface, it must be set up w/ ip address [ip] [subnet mask] and enabled using the no shutdown command. 
* use show ip interface brief to verify the interface settings on the router.

* Each network would have its own, ip address, and the gateway would have its own interface.

* IP address 10.0.0.1 / 10.0.0.2/ 10.0.0.3/ these are all endpoints, on the same network.

## Loopback interface

* **What is it used for?**: Loopback is a logical interface that is not assigned to a physical port.
* The interface can be used to test and manage Cisco IOS devices because it ensures that at least one interface will always be available, we can plug anything into it, but we can assign an IP, its used as an identifer for other processes.
* It can also be used in the OSPF identification process.
* **a loppback interface should not be confused w/ loopback address**

## loopback interface configuartion
A loopback interface is often configured durin the intial router configuration, mainly for testing purposes, the interface is configured to automatically be ready for operation.

* A router can bhave more than one loopback interface enabled, simutaneously, but each interface must have a unique IP.

# Routing Process
* **The Router Process**: The routing process involves selecting a path for the delivery of packets across different networks, from source to destination through layer 3, its like sending a letter, our network packets are the mail, and its is sent to the correct IP address via the router shipping it out.
* Routers can route packets to directly connected networks w/o required configuration. However, if the networks are not connected, the route needs to be learned. 
* **Routing decisions are made based on a routing table**

* Simiarlay to a MAC Address table, that just as the mac table learns new mac addresses when it is plugged in, the routing table keeps track of network ip tables for whole networks, which gets stored

## Routing Process

1. **Examination**: The Router examines the layer 2 address to decide if the packet was intended for itself ( the default gateway) and verifies the integrity of the frame using the FCS ( layer 2 trailer).
2. **Decapsulation**: The router de-encapsulates IP packet from the exisiting Ethernet frame and discard it. Revealing the packet, it performs and IP Header Checksum. If the checksum is correct then it will process the IP packet, otherwise drop it.
3. **Decision-Making**: The Router decides where to forward the packet based on its destination IP address and the routing table.
4. **Encapsulation**: The router will take the IP packet and decrease the time to live(TTL) field by one to avoid routing loops, then will take the IP packet and put it in a new ethernet grame w/ its own address as the next hop MAC as the destination.
5. **Forwarding**: After a decision is made, the router forwards the packet to the interface from which the packet must exit.

## Routing Choices

1. Same LAN: If the destination IP is on the same LAN as the source device, there is no need for routing. The frame will get to the destination via the switch.
2. Known Route: If the destination IP is on a different LAN,but the network device has a static or dynamic route to the destination IP, it will forward the packet to the next hop, based on the route.
3. No Route: If there is no static or dynamic route in the network devices routing table, it will forward the packet to its deafult gateway, if its unkown doesnt know how to send it, it will send it out its own backdoor, its basically the internet.
4. No Gateway: If there is no "gateway" and the destination packet is not listed, the router will discard the packet.

## Routing Table
The routing table cotains data stored in the router, w/ lists of routes to possible network destinations, the table includes info about network topology, the codes on the left side of a route show how the network is learned by the router., the command show ip route diesplas the routing table and is run in the enable mode.

## Routing Table Codes

* **Directly Connected / Local Route**: When routing table is inspected, records identified by the codes C or L indicate directly connected networks. The codes mean the devices are connected to the phyiscal layer. The C and L records are automatically created
* **Static Route**: Static routes are configured and recorded manually and are identified in the routing table by the letter S.
* **Dynamic Route**: This is like a gps, Dynamic routes are identified w/ unique letters that indicate the dynamic protocol, as follows,
1. D = EIGRP routing Protocol
2. O = OSPF routing protocol
3. R = RIP routing protocol

## IPv4

* The subnet mask is required to make the determination on if the ip can route.

* **IP**: IP, or internet protocol is a numerical label assigned to devices connected to a network, its used for host identificaiton and communication. 

* IP address space is managed by IANA(Internet assigned numbers authority) and divides into five regional internet registries ( RIRs) each responsible for their designated terrirtories.
* **Each RIR is responsible for address assignment to users and service providers.**

# IPv4
* **IPv4 Addresses**: IPv4 addresses consist of 32 bits and are divided into four octets, each containing 8 bits. This addressing method provides 4,294,967,296(2^32) IPv4 addresses in total

* AN IP address represented in a binary will appear as follows: 192.168.1.1 = 11000000.10101000.00000001.00000001

* **IPv4 Structure**: An IPv4 address consists of two parts: network and host, defined by the subnet mask.
* **Network**: Represents the network part of the IP address.
* **Host**: Represents the specific device on the network segment.

## Subnet Mask
* **Subnet mask**: is a 32-bit adress, as as an IP address.
* like an IPv4 address, a subnet mask consisits of four octects serparated by dots.
* **two similar IP addresses can belong to completely different networks, depending on the subnet mask.** 

* its like a template, it follows a similar structure
## Classful Addressing

![Alt text](assets/Subnet%20Table.PNG)

* Class A is our biggest subnet, it can have lots of hosts on it
* Class C is our smallest subnet
 * their size is determined by the subnetmask,
 255.0.0.0,

 * 255 is our largest number we can add in 8 bits. which is the binary of 8, 1's followed by 24 zeros because of the other 3 octets.
 ![Alt text](assets/subnet%20table%20explained.PNG)

 ## Communcation Types

1. Unicast: The most basic form of ip communcation is one on one, where packet is sent directly from one device to another device on the network. A single source communicates w/ a single destination.**one-to-one**
2. Multicast: Multicast is when a single source communicates w/ multiple destinations. A packet is sent from one device on the network to a group comprised of one or more devices, using class d addresses.( Streaming services)**one to many**
3. Broadcast: broadcast is when a packet is sent from one device on the network to all other devices on the network, usning a generic broadcast address, (255.255.255.255 or FF:FF:FF:FF:FF:FF) **One to all** in the same network, DHCP is a broadcast, the host is looking for the broadcast of DHCP on its local network.

## IPv4 Link-Local

* Link local addresses also known as APIPA addreses, which started for automatic private IP address, only are valid for communication within the network broadcast domain, the entire 169.254.0.0/16 address range is reserved for link-local.
* If the DHCP is not available or an IP is not statically configured, the OS will randomly generate a link-local address.
* Link-local addresses are not guaranteed to be unique outside their network segment, which is the reason why routers do not forward their packets.

## Loopback Address

* **Loopback Address**: represents teh same interface in a computer, in IPv4, an entire network (127.0.0.0/8) is reseerved for loop back addresses. 
* Almost all leading operating systems use the name "localhost" to represent the IPv4 loopback address 127.0.0.1
** IPv6 address reserved for loopback is 0000:0000:0000:0000:0000:0000:0000:0001/128

## Public vs. Private

* **Private**: Private IPs are non-unique addresses that can belong to one of three IP address ranges. They are used to create networks that do not communicate over the internet, the same private IPs can be found in multiple separate networks and are free to use.

* **Public**: Public addresses are used for communcation over the internet. These IP addresses must be unique, require a fee, and be purchased from service providers. A router will typically have voth a private and public IP. For ex. the address 8.8.8.8 is a public address used by google.

## Private IP Ranges
![Alt text](assets/Private%20IP%20range.PNG)

# IPv6 
 Over the years, The IPv4 address space was deplated, since technical progress meant that many more devices around the world were connected to the internet.
 * IPv6 was designed to solve the IPv4 address space limitation and provide additional enahcnements. IPv6 has a larger 128-bit address space, w/ the number of avbailable addresses being 340*10^36, 340 undicillion.

## Compressing IPv6 Addresses

**IPv6 Addresses are long and fifficult to read, some rules exist to omit specific numbers to simplify the addresses.**

1. Full Address: A full address contains all eight blocks with four hexadecimal digits.
EX: 2001:0000:3238:0001:0063:0000:0000:FEFB

2. Leading Zeros: The first rule allows us to discard leading zeros in a block, making the address a bit shorter. Drops the leading zeros
EX: 2001:0:3238:1:63:0000:0000:FEFB

3. Consecutive Zeros: If two or more blocks contain consecuvtive zeros, they can be omitted and replaced w/ double colon signs (::), note that omitting is allowed only once in the address.
EX: 2001:0:3238:1:63::FEFB

4. Zero Block: If there is a block that consists of four zeros but w/o consectutive zero-filled block, it can be replcaed w/ a single zero, and final address.
EX: 2001:0:3238:1:63::FEFB

## IPv6 Address Breakdown

![Alt text](assets/IPv6%20Breakdown.PNG)

## Configure & Verify IPv6

* To enable IPv6 Routing, enter the configuration and terminal mode and run the ipv6 unicast-routing command
* Configure IPv6 on the router interface using the ipv6 command

* Verify the configuration using the show ipv6 interface brief

## Device Communcation Types

* **Unicast**: Unicast addresses represent specific network interfaces that support IPv6, unicast addressses have three sub-types (described in the following slide)

* **Multicast**: Addresses used to send IPv6 packets from a single host to multiple destinations

* **Anycast**: anycast refers to IPv6 unicast addresses that can be assigned to multiple devices. Packets sent to an anycast address are routed to the nearest device that has that address(whichg is why anycast is known as the one to the nearest) This method operates like IPv4 broadcast.

## IPv6 Unicast Types

![Alt text](assets/IPv6%20unicast%20types.PNG)

* Global unicast, similar to unicast addresses to IPv4 public addresses, theyre unique and can be routed via the internet. IANA currently assigns only 200::/3 address

* Link-Local, addresses that enable communication between devices in the same local link ( LAN) link local addresses must be unique only within the link, they arent guaranteed to be unique beyond their network segment and begin w/ FE80::/10.

* Unique-Local: Similar to IPv4 private addresses w/ minor differences, unique addresses shoud not be routable in the global ipv6 and should not be tranbslated to global ipv6 addresses, they begin w/ FC00::/8.

## IPv6 Address Example

![Alt text](assets/ipv6%20address%20examples.PNG)


## IPv4 & IPv6 Coexistence

* IPv4 and IPv6 can coexist using protocls and tools created by IEFT, which are kown as dual stack, tunneling, and translation.

* **Dual Stack**: Dual stack means that a device runs both IPv4 and IPv6 protocols simultaneously. using two stacks allows both ip versions to coexist.

* **Tunneling**: Tunneling is used when IPv6 addresses are to be sent over the IPv4 networks or vice versa. In this method, the IPv6 packet is encapsulated within an IPv4 packet.

* **Translation**: Translation allows IPv6 to communicate w/ IPv4-enabled devices using technqiues similar to those utilized by NAT.