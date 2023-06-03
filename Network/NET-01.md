# Introduction to Networks

## Table of Contents

1. Network types & devices
2. Network media & cables
3. Network topologies & archeticture 
4. Network protocols & commands
5. Network technology

* Networking is moving data, 1's and 0's across end to another, this is to share data.


# Network Types & Devices

## Common Types of Networks

* LAN ( Local Area Network) defines a small geographical area in which multiple computers and other devices are connected. LANs can be setup in homes and small businesses and can be managed individually or centrally.
* WAN ( Wide Area Network) is spread across an unlimited geographical area and connects between multiple LANs. WANs are usually managed by service providers.


LANs can be designed to use one of two communications **wired** or **wireless**

## Other Types of Networks

* MAN (Metropolitation Area Network ) larger than a LAN but smaller than a WAN. In most cases, it is managed by a city municipality and enables connection to broader networks.
* SAN ( Storage Area Network ) is a dedicated network that supports file servers and provides efficient transfer of unusually large data sizes at extremely high rates.

SAN is often not regarded as a type of network bedause it is closer to being inftrastructure.

## Network Structure
* Network requirements: Communication among devices can be as simple as connecting a cable between two computers.
* on the other hand, it can be as complex as a large assembly of multiple networks spread around the world and regulated by a variety of sophisiticated devices and protocols.
* The history of computer networks began in the 1960 w/ a network called ARPANET.

## Network Devices

* **End Devices** : Devices that connect to a network for communication purposes, such as computers, phones, and others. All end devices have unique addresses that identify them on the network.
* **Media**: Media, based on the word medium (meaning in between) is a means of transferring data, such as metallic wire, glass, plastic, wireless radio frequencies, and others.
* **Intermediary Devices**: aka Network Devices that transfer messages over the network and faciliate commnunication between end devices. These move thoses 1's and 0's across the network 

 ## End Devices
 * In todays world, most people communicate with each other through networks,
 * End devices are source or destination devices in a networked system.
 * Computers, laptops, and phones are end devices that allow us to communicate over a network.
 * End devices must have the ability to connect to a network via an **NIC**, to be able to send and receive information.

## Network Interface Card ( MEDIA )

* To allow an end device to send and receive information over a network, it must have the appropiate hardware. 
* A (NIC) network interface card allows end devices to interact w/ other devices over a network
*other NIC names are
1. network adapater
2. LAN adapter
3. Physical Network Interface

## Intermediary Device

* Intermediary devices act as bridges, interconnecting end devices.
* Smart intermediary devices know how to differentiate between devices and can send data to specific destinations.
**unlike smart devices, simple intermediary devices send information indiscriinately across a network

## switch
* for a multiple end devices to communciate with eachother, a mechanism needs to be setup to handle the transfers.
* A switch is a device w/ physical ports to which end devices can be connected via ethernet cables, to create a network.
* Switches use MAC addresses to pass information from one end device to another

## Switch Types

* **hub** a hub is the legacy implementation of a switch. it broadcasts data to all connected devices, as opposed to sending information to dedicated destinations.
* **Layer 2 Switch**: that is most common and basic switch in use. it uses MAC addresses to forward information to specific destinations within the network.
* **Layer 3 Switch**: a layer 3 switch eprforms the same operations as a layer 2 switch but can also 
funcation as a router if it is configured to do so.
**layer 2 vs 3 is a big for network+**
* there is communication all among the network, and the switches are used to allow the network to communciate via MAC address w/ the correct interface connection.
* Switches serperate **collision Domains** 

## Broadcast & Collision Domains
* A collision domain is a group of nodes that can "hear" eachother. Ideally, when one node talks, all the others only listen. When two nodes talk at the same time, a collision occurs, to resolve this issue, a hub creates collision domain.
* A switch, which operatoes in Layer 2 of the OSI model, can create seperate conversations between nodes, which, in turn, creates serparate collision domains.
* although, collisions are expected to occur in a half-duplex ethernet network, if a collision domain becomes too big, traffic problems will arise, due to retransmissions.
**routers separate broadcast domains**
**switches separata collision domains** 
* **Communication**: Broadcast is a type of communciation whhereby the sender sends a single copyof the data to all devices on the same network segment.
* Broadcast communciation must be used, since protocols such as ARP and DHCP rely on it.
* A broadcast domain includes devices that receive broadcast packets originating from senders within the same network segment
* A Router operatoes in the network layer and separate both collision domains and broadcast domains.

## Duplex Modes

* telephone vs wakie talkie
* **half duplex** only one party can send or receive data at a single moment. For example, a walkie-talkie works in half duplex, only 1 party can talk at a time.
* **Full duplex**: both parties can send and receive data at the same time. ex. a phone call is performed in full duplex, data flowing back/forth simuntaniously 
* When 2 devices are set to different duplex modes, a duplex mismatch occurs, this reduces the quality of the communication
## Router

* While switches allow devices to interact in the same network, **routers** allow them to communicate w/ different networks.
* A router connects networks and allows communication betweend end devices in different networks.
* routers use IP addresses to route information among networks.
* Switches use MAC addresses to forward traffic, Routers use IP addresses to forward traffics. Switch layer 2, Router layer 3.

## Other Devices
* **access points**: AP's allow end devices to connect to a network wirelessly and manage information transmission. a wireless device user can connect to a wired network via a properly configured access point, its a wireless switch.
* **Firewall**: Firewalls are effective security tools against threats that originate from outside a network, filtering traffic that allows or blocks the transfer of info, its usually in the peremiter of the network, but now we are integrated within the entire network, even the internal network to separate for security control.
* **WLC**: A Wireless LAN controller allows the configuration of mulitple APs to be managed from a central device, this is a useful in large organizations where multiple APs are deployed in different sections of a building. Its like a special built server to configure each AP, instead of managing each one individually.
* **Home Router**: The home router combines the feature of all the intermediary devices covered in this lesson so far, in a single device. It acts as an AP, a switch/firewall with the most basic configuration.

**network+ you have to look where the coverage goes beyond, we have a big buidling, where a ap is covering outside the coverage point, making sure the AP isnt broadcasting outside of the area. the coverage leaking out of the area**

# Network Media & Cables

## Media

* information cannot be transmiitted over a network without a means of transportation. 
* the term media refers to the physical cables or wireless  technologies used to pass the information from one device to another.
* Different types of media feature varying speeds and distances of data transfers.
**connections between continents were made possible using "submarine cables" that were stretched across thousands of kilometers through the oceans.**

## Eternet Cable

* ethernet cables, or catergory cables, cat 5, cat 6
* copper cables, signal deteriorates as the distance grows, and due to the influence of RFI and EMI, which limit cable lengths, also patch cords/cables.

## Ethernet Cable Types
* all have a max distance of 100m's or 300 ft
* CAT-5: Max speed of 100mb/s
* CAT-5e: Max speed of 1gb/s
* CAT-6: Max speed of 1gb/s , supports 10gb/s for 55m
* CAT-6a: Max speed of 10gb/s
* CAT-7: Max speeds of 10 gb/s, supports 100gb/s for 50m

## Ethernet STP & UTP
* UTP: unshielded twisted-pair, is the most common copper cable in use. It consists of four twisted pairs of colored wires, the act of twisting the wires is done to prevent signal disruption (cross-talk)
* STP: Shielded Twisted-Pair cables are similar to UTP but have additional protection against EMI and RFI interferences, each twisted pair is wrapped in foil.
* **EMI and RFI are electromagnetic and radio frequency interferences that can affect signals**

## Ethernet Cable Configurations
**this will be on network+, to configure the cables**
* **straight-through**: wires are placed in a straight formation from side a to side b, this form is used for cales that are meant to connect network devices of different types, such as a switch and endpoint.
* each cable is connected stragiht to the matching pin on the otherside.

* **crossover**: Wires crisscross from Side a to Side b, this form is used in cables that are meant to connect similar network devices. when 2 computers are being connected together that is why we have to crossover thats because it can transmit the data to have it flipped so it can receive.

# Network Topologies & Architecture

## Network Topology

* A network topology describes the structure of a network, it represents all the connections between all components in a network, several types of topologies can be used to contrsuct networks.
**a topology represents the resource of a network, but not locations and distances.**

## Network Topologies

* **point to point**: A connection between two computers,networks, or other devices. If connection fails, the communication is disrupted.

* **star**: In a star topology, all end devices are connected to a central intermediate device.  This type of topology is easy to setup and maintain, it is highly scalable.
* **mesh**: In a mesh topology, each end device can have multiple connections to other end devices. This configuration is highly resilient due to its allowance of mulitple connections, but it is also expensive and very difficult to maintain.
* **Hybrid**: A hybrid topology is a combintation of other topologies, although a hybrid configuration takes advantage of the strong points of other topologies, it also has to deal with the disadvantages of those topologies.

## 3-tier architecture

* the concept of a 3-tier architecture can be applied to any type of network. 
* the modfel helps design, implement, maintain a scalable, reliable, and cost -effective network.
*its simplistic structure akes it very easy to manage, the combination of these attributes means that it is the best choice for large enterprises, in which thousands of computers need to be interconnected, sometimes over an area that includes several buildings.
**each layer has its own features and functionalities, which reduces network complexity.

* 3-Tier Architecture consists of three layer that provide isolation between devices, greater flexibility, more security options and resilience.
* The separated layers are:
* **core**: routing layer connecting to servers and the internet
* **distribtuion**: serparation between core and access layers, and boundary control
* **acces**: Communication between end devices
* the layers can be managed independently without affecting other layers.

## Collapsed Architecture

* Similar to 3-tier but has different number of layers and a different scalability potential.
* This architecture, the core and distribution layers are collapsed together to form a single layer.
* this means it has the advantages of the 3-tier architecture, but has smaller network scale.

## Physical & Logical Addressess

* When the first networks were created for local computers to communicate with eachother and hare data, design engineers realized they needed to know how computers would talk to each other and who they could talk to.
* the idea was for each computer to have a unique name or identification, and the conecpt of a MAC address was born.
* A MAC address is the unque identity of a computer within a network, while ip addresses are used to identify machines operating in different networks.
* **Each network card in a device has both a MAC address and an IP address at any given moment.**

## Physical Address

* A MAC address is a unique hardware identifer attached to each network card, the address is static and should not be changed.
* It consists of six hexadecimal nodes ranging from 00 to FF.
* A Mac Address includes 2 parts
1. the first three nodes represent the manufacturers identifier
2. the last three nodes represent a serial identifier.

## Internet Protocol

**An IP is used to uniquely identify computers on the network and create network partitions.**

* **IPv4**: IPv4 addresses are the most common today, they consist of four octets of numbers between 0-255, which can generate approximately four billion ifferent addresses.
* Some addressses, such as X.X.X.255, are special, while others such as 192.168.X.X, are dedicated to specific users.

* **IPv6**: Due to advances in technology, IPv4's four billion addresses were threatended with depletion, and IPv6 was developed w/ 6 hexadecimal octets that can generate aopproximately 340x10^36 addresses
* IPv6 addresses have not yet been fully integrated in modern use cases.

## Network Classes

* Subnet masks define which addresses in an octet can be used in an IP address, while remaining on the same network.
* Devices ( Computers or network ) must be in the same network and subnet to communicate without routing
* The first IP address of each subnet is the network address and cannot be used for hosts or devices.
* The last IP address of each subnet is the broadcast address and cannot be used.

# Network Protocols & Commands

## Communication Protocols

* Protocols: To properly communicate with eachother, different devices require protocols.
* Protocols are predefined set of rules descriing how something should work or behave.
* Protocols help maintain order among different technologies
* **protocols can be considered 'language' of data transgfer, to communicate properly, two or more devices must first agree to use the same 'language'.

## Network Protocol

* **IP**: Internet Protocol, is used toi establish communication over the network, w/o delivery verification.
* **DNS**: Domain Name Service, a protocol used to translate domain name to IP addresses, and vice versa.
* **DHCP**: Dynamic Host Configuration Protocol, is used to allocate IP addresses to new computers that join the network.
* **HTTP**: Hypertext Transfer Protocol, used to transfer text-based data,such as webpages, over the internet.
* **HTTPS**: Hypertext Transfer Protocol Secured, is an implementation of HTTP, it encrypts the transferreed data to prevent it from easily being read in plain text or leaked.

## Network Commands

* The importance of Commands
*  Commands are used in network configuration, maintenance, troubleshooting, and more.
* It is essential for any network to frequently run commands that check the state of the network and monitor it.
* Although some systems enable network configuration via a GUI, the configuration is still often done via the CLI.
* **an example of a powerful use of network commands is for error detection**

## Ping

* Ping x.x.x.x

* Ping is the most common command in administrative networking activity
* It is used to check connectivity between computers over the network, it also provides information such as connection speed and reliability
* It sends out 4 echo requests to test that the remote host is online and reachable.

**tracert** will show us the packet that follows it to its destination

* ## IPconfig
* IPconfig displays a computers IP configuration
* It can also request a new IP address, if DHCP is configured.

-commands-
* Ipconfig /all = displays extended information
* ipconfig /release = drops an IP address
* ipconfig /renew = requests a new IP address

## NSLOOKUP
* ns = name server lookup
* NSlookup x.x.x.x

* Computers use IP addresses to communicate with each other, while humands use names that are easier to remember than numbers.
* nslookup sends a query to get the name of a computer by its IP address, it can also do the opposite query an IP address by the domain name.

## TRACERT

* tracert x.x.x.x

* Information in the network passes through multiple stations on the way to its destination.
* tracert displays all the stations along the route taken by the information to its destination
* it can work w/ a domain name or an IP address.

## NETSH

* Netsh [ command \ option ]
* A fast way to configure network information is to use the netsh command.
* it alows the confoiguration of the IP address, DNS, default gateway, and various network functions
* the example on the right shows how to set up an IP address and verify settings using netsh.






**MAC address are usally 48 bits.

