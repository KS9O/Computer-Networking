# Dynamic Routing

## Table of Contents
1. Dynamic Routing concepts
2. RIPv2(routing information protocol)
3. OSPFv2 (OnShortestPathFirst)

# Dynamic Routing Concepts

* **Whats Dynamic Routing**: The purpose of this protocol is to map networks and update routing tables w/ the shortest routes in a fully automatic and independent matter.
* thE method is made possible by special algorithms and protocol packets.

# Routing Table 
* the show ip route comand output lists which local and remote networks the router "knows".

## Routing Source Codes

* **S**: inditicates a static route
* **D**: inditicates the route was learned dynamically from another route using the EIGRP routing protocol, Enhanced interior gateway protocol.
* **OSPF**: indicates the route was learned ynamically from another routing using, on shortest path first, routing protocol
* **R**: Indicates the route wasa learned dynamically from another router using the RIP routing protocol, routing information protocol.

## Key Elements

* Fits any Topology: Once the protocols are activated, the routers begin "talking" to each other and map the network topologies themselves.
* Fast and Independent: Dynamic routing is based on software that can gather a lot of information in a short time and input it to an algorithm that computes the information to find the fastest route to each network.
* Awareness: Each dynamic routing protocol uses timers that detect any change in the topology, such as a connection failure. When a change is detected and involes a network failure, the protocols will search an alternate path.

## Administrative Distance (AD) Values
![Alt text](assets/Administrative%20Distance%20(AD).PNG)

* **AD is a predefined value, the follow table lists the default AD values for different routing methods.**

## Metrics

* **What is a Metric?**: A metric is a measurable value assigned by the routing protocol to different routes based on the usefulness of the route.
* When there are multiple paths to a remote network in the same protocol, routing metrics are used to determine the overall "lngeth" of a path from a source to destiniation.
* routing protocols determine the best path based on the route w/ the lowest metric value.

## Routing Protocol Metrics

![Alt text](assets/Routing%20Protocol%20Metrics.PNG)

## Protocol Types

* **IGP vs. EGP**:
* IGP, Interior Gateway Protocols: are routing protocols used within an autonomous system, which is a group of networks (AS) such as company routers.
* EGP, Exterior Gateway Protocols: are used to map routes between autonomous systems and are mainly utilized by ISPs.
* **Distance Vector vs. Link State**: The fundamental difference between distance vector and link state routing protocols is how the protocols discover the topology and the way they share routing information w/ the routers.
* **BGP is a classified as a path vector protcol and is used to map the internet.**

![Alt text](assets/Protocol%20Classification%20Table.PNG)

## Distance Vector

* Distance Vector: is a routing algorithm that calculates the best path for a packet based on the factors of distance and vectors, only from what was given, they dont know the topology at all, we dont know the actual path we just know there will be a sign to direct us to our destination.
* Distance: the distance between the router and the dfestination network, based on the metric of number of hops(routers)
* Vector: the outgoing interface and the direction to the path that leads to the destination network.

## Link State

* Link State: routing protocols include complete network topology maps, 
* Network Map: The map is created based on information from all routers on the network.
* Network Changes: Link state routing protocols do not broadcast information regularly, updates are only sent when a change occurs on the network.

## Passive Interface Diagram

![Alt text](assets/Passive%20interface%20diagram.PNG)

* **Passive Interface Feature**: Passive interface is a feature used in all routing protocols, its purpose is to disable routing updates on specific interfaces, which decreases usage and increases security. The command syntax is the same in all routing protocols, its a typically placed on interfaces facing the LAN.
* **Passive interfaces should not be configured between routers.**

## Why use Passive Interfaces?

* Bandwidth: Dyanmic routing updates consume bandwidth because messages are sent in broadcast or multicast, causing switches to broadcast to all ports.
* Resources: Devices in the same LAN must process updates to layer 4 (transport layer) and only then discard the update.
* Security: Packet sniffing software can be used to intercept packets that include routing updates and redirtect traffic by corrupting the routing table w/ false metrics.

## Classful & Classless Routing Protocols

![Alt text](assets/classful%20and%20classless%20routing%20protocols.PNG)

# RIPv2

* **Routing Information Protocol**: It is a distance vector protocol, and its metric method is hop count, the protocol has limitations, such as a the maximum allowed hops for a route, which is **15**. Due to its limitations, it is often implemented only in small networks that do not require a high level of scalability. Unlike other protocols, RIP operates in layer 7 (OSI) and uses port 520 (UDP)
* **There are three verisons of the protocol. RIPv2 is the most widely used but is not the most popular due to its inherent limitations.

## RIP Version Comparison

![Alt text](assets/RIP%20versions.PNG)

## RIP Parameters

* Administrative Distance: RIP's default AD value is 120, the value can be modified, but it is not recommended to do so.
* Metric: RIP determines the shortest route to a network by the number of hops (routers)to the target network, the route w/ the least amount of hops is added to the routing table, RIP supports routes of up to 15 hops.

## RIP Timers

* Update: By default, the update value is 30 seconds, and messages will be broadvast/multicast on a RIP-enabled interface.
* Invalid: Invalid is also known as an expiration timer, by default its value is 180 seconds, after which the routing entry will indicate the destination is unreachable.
* Flush: If a route is invalid after 180 seconds, it will remain in the routing table for an additonal 60 seconds before it is removed and its neighbors are informed of its status. this is to slow things down for 180 secs then it will accpect the changes.
* Hold-down: the default value is 180 seconds. During this time, the router will not accept new updates for the route.

## Auto-Summary

* **Auto-Summary Feature**: Auto-summary isa feature that allows automatic summarization of routes to their classful networks, this enables multiple networks to be represented w/ a single summary address.

* By default, RIP and EIGRP summarize subnets exceeding the classful boundaries to a major classful network address in the routing updates.
* **This feature is often disabled because most address schemes in networks today do not allow address summaries w/ compromising communciation** 

## Network Topology Example

![Alt text](assets/Routing%20topology%20example.PNG)

* Convergence: is when every router can reach any network, everything has been updated and reaches every router.

## RIPv2 Config Ex.

* RIP COMMANDS
1. R1(config)#router rip
2. R1(config-router)#version 2
3. R1(config-router)#no auto-summary
4. R1(config-router)#network 192.168.10.0
5. R1(config-router)#network 172.16.0.0
6. R1(config-router)#network 172.16.0.8
7. R1(config-router)#passive-interface gigabitethernet 0/0, or g 0/0

* R2(config)#router rip
* R2(config-router)#version 2
* R2(config-router)#no auto-summary
* R2(config-router)#network 192.168.20.0
* R2(config-router)#network 172.16.0.0
* R2(config-router)#network 172.16.0.4
* R2(config-router)#passive-interface gigabitethernet 0/0, or g 0/0

* Router rip: enables and enters rip config mode.
* version: sets the rip version
* network: advertises the network and enables RIP updates on the network interface
* no-summary: disables the auto-summary feature.
* passive-interface: disables RIP updates on the interface

## Verify RIPv2 on R1
![Alt text](assets/Routing%20R1%20Table.PNG)

* R1s routing table after RIP finished updating it, **R** represents the route learned by the RIP protocol
* An important feature is that if the router finds two equal paths to the network, both routes are added to the table, and load balacning is applied, look at 172.16.0.4/30
there are 2 possible paths to this network. When a router has a route of 2 equal costs, the 2 numbers we see, 172.16.0.2 and 172.16.0.10, this will be added to the table by RIP to have rudandant paths and do load balance, where it sends packets in opposite directions. We make load balacnce on the bandwitdh and our traffic on the network.
## R2 and R3 Verification
* The rip flag shows only RIP entries in the router table.
* Another method is to cehck the running-config file to view the current configuration 
![Alt text](assets/R2&R3%20verfication.PNG)

## Show IP Protocols

* Show ip protocols displays the current protocol settings, this is valid for every dynamic routing configuration, such as OSPF.
* The output includes:
1. Timer information
2. Advertised networks
3. Passive interfaces
4. More
**command**: R1#show ip protocols

## Routing Table Entry

1. Route source
2. The destination network address/prefix
3. The AD and metric of the route
4. Next-hop address through which the packet passses to the target network
5. the route age (timestamp)
6. the local outgoing interface that points to the target network
R1#show ip route
* R 192.168.20.0/24 [120/1] via 172.16.0.5, 00:00:09, Serial0/0/0
## Gateway of Last Resort
* Static Default Route: the static default route redirects packets w/ unkown destinations to the gateway of last resort, which is a router that communicates in a specific direction (typically to the ISP). RIP can set the default so that it will have the routes sent to a specific R1 for a path. We will choose a specific router to be our gateway of last resort, and the other routers will send data/packets to that labeled router so that it can be sent to the internet, send all the default routes to the main router we selected to be our gateway of last resort.
* Propagating Default Routes: Each routing protocol shares its default routes w/ all routers on the network through protocol updates.

# OSPFv2

* Open shortest path first: OSPF is a link state routing protocol introduced in 1989 w/ more advanced features, making it a strong and scalable solution forany size network. OSPF was designed as an alerternative to RIP
* OSPFv2 was released in 1991 and is still used today
* OSPFv3 was developed for IPv6 in 1997.

## Topology Changes & Timers

* Monitor the Network: OSPFv2 keeps track of changes in the topology, such as when a new network is added or a link fails.
* Hello intervals: " Hello " packets are sent every 10 seconds to all OSPF-enabled routers.
* Dead Intervals: When a router doesn't receive a "hello" packet from its neighbor within 40 seconds, it will consider that neighbor "dead" and will start looking for alternative routes.

## OSPF Packets

* **LSA**: Routers use **Link State Advertisement** to advertise the routing topology to all other local routers in the same OSPFv2 area, LSA are sent in multicast.
* **LSDB**: **Link State Database** stores received LSA packets after the routers enable OSPFv2 to use the SPF algorithm to calculate the routes.
* **DBD**: When an adjacency is initialized, OSPFv2 exhanchges **Database Descripiton** packets to describe the content of the topological database
* **LSR**: If a router notices that parts of its topological database are outdated, it will send a **Link State Request** to a neighbor for more updated versions of those components, LSRs are sent in multicast.
* **LSU**: **Link State Update** messages are responses to LSR messages, LSUs are sent in unicast. 

## SPF Algorithm and Tree
* Dijkstra: we calculate all routes to each network in the topology using the Dijkstra algorithm, OSPFv2 creates a map of the network called an SPF tree.
* The SPF tree is stored in a database on the router called a link state database (**LSDB**)
## OSPF Metric
* **Best Route Determiniation**: OSPF basses its metric calculation on the bandwidth of the links along the path to the destination.
* **Cost**: All bandwidth information recorded for the route is calculated using the OSPF formula (all considerations are summed), resulting in the cost value.
* Cost Calculation: Reference speeds (MBps) 1000 / Interface speed (Mbps) 100 = Link Cost 10

* **The default reference speed is 100 mbps and can be adjusted using the (auto-cost) command**

## Wildcard Masks
* Mask Inversion: wildcard masks are used in some routing protocols, such as OSPF, as inverted subnet masks.
* For ex. the subnet 255.255.255.0 inverts to a wildcard mask of 0.0.0.255.       255.255.255.0= 0.0.0.255
* Binary equivalent = 11111111.11111111.11111111.00000000 = 00000000.00000000.00000000.11111111
## Router ID
* **Router ID**: When OSPFv2 is enabled on an interface, the router must determine if there is another OSPFv2 neightbor on the link. Router Ids are set **manually** and used to uniquely identify each router.
* **First Fallback**: If no router ID is configured, t he highest IP address of any router **loopback interface** is selected as the router ID.
* **Second Fallback**: If no loopback interface is configured, the highest IP address among its **active interfaces** is selected as the OSPFv2 router ID.

## OSPFv2 Areas
* What is an Area?: OSPF uses a concept called **areas*, A single AS or full topology can be divided into smaller areas.
* Dividing the topology into areas reduced router resource consumption and protocol response time.
![Alt text](assets/OSPFv2%20Areas.PNG)

* Single-Area OSPF: For small to medium-sized networks that use a single area, the default OSPFv2 is **AREA 0**. the maximum recommended area is 50 routers.
* Multi-Area OSPF: In larger networks that require more areas, **Area 0 will be the backbone area**, and all routers outside that area will be assigned other unique numbers (1,2,3,etc.)
* Area border router is responsible for sharing the area with other routers
* **Routing between areas is done by an ABR(Area Border Router)**

## Area Advatanges and Disadvantages

![Alt text](assets/Area%20Advantages%20vs%20disadvantages.PNG)

## Network Topology Example

![Alt text](assets/OSPF%20Routing%20topology.PNG)

* Networks A, B, and C cannot reach each other because the router doesn't know each other yet.
* Once OSPF is enabled on all routers, they will start to share routing information.
* Next, each router adds remote networks to its table, for example, R1 will add Nets b and c
* Again this process is called, convergence, where any router can reach any network!

## OSPFv2 Config Ex.

* router ospf enables OSPF and enters OSPF configuration mode, router-id sets the roter OSPF identifier.
* network advertises the network and enables OSPF updatse on the network interface
* area sets the interface area ID
* auto-cost sets the reference bandwidth calculation
* passive-int disables OSPF updates on the interface
* a log messager indicates a link to another SOPF-enabledd router.
* **COMMAND**:

1. R1(config)#router ospf 1
2. R1(config-router)#router-id 1.1.1.1
3. R1(config-router)#network 192.168.10.0 0.0.0.255 area 0
4. R1(config-router)#network 172.16.0.0 0.0.0.3 area 0
5. R1(config-router)#network 172.16.0.8 0.0.0.3 area 0
6. R1(config-router)#auto-cost reference-bandwidth 1000
7. R1(config-router)#passive-interface g0/0

## Verify OSPF on R1

* we are looking for O's which represent the route learned by the OSPF protocol
* An important feature of OSPF routing is that if the router finds two equal paths to the network, both routes will be added to the table, and laoad balacning will be applied. 
![Alt text](assets/Verifying%20OSPF%20Table.PNG)

## Show IP Protocol
* Show ip protocol, displays the current protocol settings
* show ip ospf interface displays the timer information.
* show ip ospf neighbor displays adjacent OSPF-enabled routers.