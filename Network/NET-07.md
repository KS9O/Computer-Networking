# IPv4 & IPv6 Static Routing
## Table of Contents
1. Router Operation
2. Ipv4 Static Routing
3. IPv6 Static Routing

# Router Operation

* **how a router operates**: One of the routers main jobs is to select the best path for a packet.

* The decision is based on its destination address.
* After determining the best path on which to forward the packet, the router encapsulates the packet in a new frame in accordance w/ the relevant outgoing interface.


## Packet Forwarding Review

![Alt text](assets/Packet%20forwarding%20review.PNG)

## Remote Networks

* **What is a remote Network?**: A routers best routing decision is based on its routing table. But where does the routing table get its information from?
* Networks connected directly are added to the table immediately, but a remote network must be configured by the user.
* A remote network is any network not connected locally to the router.

* It goes from an endpoint to the default gateway then goes to the network, this is a remote network, could be internal or external.

* **The ICMP message "destination unreachable" is displayed whenever the router cannot find a match for the path in its routing table.**

## Remote Network Learning

* **a remote network can be learned by a router in one of two ways: statically or dynamically.**

* **Static Method**: Using the static routing method, the user enters every network manually in the routing table. done via a network administrator manually inputting the route.
It follows the exact route we have input everytime.

* **Dynamic Method**: In the dynamic routing method, the router automatically learns the remote network from the routing tables of adjacent routers, by using various protocols.
* The routers can share w/ eachother info, so that each router can learn from one another to be able to connect to different networks, and find their paths.

## Static Method Pros & Cons

![Alt text](assets/Static%20pros%20vs%20cons.PNG)

* DYNAMIC is able to get eavesdropped in on because hackers can learn into the network.

* Static is more efficent, it doesnt have to do as much processing, less cpu and processing
* Networks become highly predictable at static methods, we can track every packet being forwarded on the network if we know the topology.
* dynamic is a lot harder because it can have the ability to change ever so often depending on the packet being sent.

## When to Use Static Routing
* **network administrators decide if and when to use Static Routing, based on network requirements.**

* **STUB networks**: Static Routing is a better choice when routing to and from stub networks, this is a one way, in and out network aka a stub network, very simple.
* Stub networks consist of a single router that sends and receives non-local traffic via a single path.

* **SMALL Networks**: Although static routing is simple and secure, and saves resources, it does not provide a sufficient level of scalability in larger networks.

# IPv4 Static Routing

* Administrative Distance (AD) is a predefined value for each routing method. The router selects the path of the lowest AD value in the routing table. For ex. If there are two routes to the same destination network, one via OSPF ( a dynamic routing protocol) and the other a static route, the router will select the static route (1 vs. 110)>

## AD Value

* **AD is a predefined value. The following table lists default AD values for different routing methods.**

![Alt text](assets/AD%20Values.PNG)

* if we have a low AD value this means that this is a very trusted route for a connection, via the router. 

* if a router is offered a static or a dynamic, the router will always go over the dynamic over to the static always as its the reliable source, as the router picks it at, or we can see how it sees it. the lower the better.

## Additional Types of Static Routing

* **Floating Static Route**: Provides backup paths to primary static routes for situations in which a link failuire occurs. This route type is only used when the primary route is not available. The AD for floating static routes is higher than the AD for primary routes. Basically we can think of this as a **backup** route. The router will only use the floating if the primary is not available.

* **Summary Static Route**: To reduce the number of routing table entries, multiple static routes can be summarized to a single address. it can convert multiple routes into 1 via them all going in the same direction.

* **Host Static Route**: Similar to standard route, but instead of configuring a network, it is used to forward traffic to a specific host. It uses a default mask of 255.255.255.255, this subnet is for a specific node/endpoint

## Floating Configuration Ex.

* **COMMAND**: Ip route < network-address > < subnet-mask> < direction > < AD >

The code on the right is an ex. of a primary and backup route configuration

The primary route is set w/ a default AD (1)

* Both routes will not both show up, only the primary route

The backup route points to the same network but from a different direction and is set w/ a higher AD (5).

**Note**: The backup route will be shown only if the primary route fails.

## Host Configuration Ex.

* **COMMAND**: R1(config)#ip route < ip-address> 255.255.255.255 < direction> (IP)

* although this type of static route is not very common, it can be useful as a redundant path to a specific resource, such as a server, this method may be usdeful for special routing requirements.

## Summary Conditions

![Alt text](assets/Summary%20Conditions.PNG)

* **Contiguous**: To summarize the network to a single address, the destination networks need to be contiguous.
* **Same Routing Path**: All networks use the same outgoing interface or next-hop address.

In this Ex. instead of four standard static routes, a single summarized static route is used, as shown in the next slide.

* all for of these networks are in the same direction, router 1 will forward it all in 1 direction, 

* We can only summarize routes that are contiguous, basically routes that are all next to eachother, we can craft a route, or a subnet range that will encompass all 4 networks, resulting in 1 ip route command.

## Summarizing Steps

![Alt text](assets/Summaring%20steps.PNG)

The easiest way is to convert the ip addresses into binary.

we line them all up, and identify all the same bits that are the same, the first 13 bits are all identical. so the first 13 bits that are all the same, we turn that back into a decimal and make that our address. 

so we would know what our summarized configuration

command: R1(config)#ip route 172.8.0.0 255.248.0.0 10.0.0.1

This ex. shows the code for summarizing and verifiyng the new route, note the prefix is 13.
![Alt text](assets/Summarizing%20Steps%20that%20explain%20it.png)

# IPv6 Static Routing

* **IPv6 Static Route Types**: Static routing is similar for IPv4 and IPv6, with the expection of how the destination network addresses are formatted. 
* IPv6 supports the same static routing types, and most of the parameters are identical to those in IPv4 commands.

## IPv6 Prerequisites 

* IPv6 packet forwarding must be enabled on the Cisco router, Command **IPv6 unicast-routing**

* The interface must be enabled and configured w/ an IPv6 address.

Command: R1(config)#ipv6 route < network address > /prefix direction

1. specifies the IPv6 remote network address.
2. Specifies the remote network prefix
3. Sets the direction of the network, which can be: Directly-connected - the local outgoing interface.

Next-hop - the IPv6 link-local or global-unicast address of the interconnected router.

## IPv6 Configuration Ex.

![Alt text](assets/IPv6%20Config%20ex.PNG)

We can create backup routes/alternative routes displaying alternative distances.

The 61 became a summarization, they took all the 64 prefixes and summarized to 61.

## Verify IPv6 Configuration
* Show ipv6 route
command: R1(config)#do show ipv6 route

remember do not use show ip route ( this displays IPv4 routing tables) rathe than IPv6 tables.