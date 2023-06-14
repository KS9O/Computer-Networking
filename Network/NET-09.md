# VLANS & Trunk

## Table of Contents
1. Virtual LANs
2. Trunk Protocols
3. Inter-VLAN Routing

# Virtual LANs

* **Virtual LANs**: VLAN is a comman concept and practice among network administrators. You need enterprise equipment to run this type of setup. Most networks today implement VLANs in one way or another. VLAN is a layer 2 feature that allows virtual network segmentation, meaning dividing a physical network into separate logical networks.
* Each logical network is a VLAN and represents serparate broadvast domain.
* **The same rules that govern LANs also apply to VLANs**

* **How do Vlans work?**: They give us a logical separation, multiple ports are configured on the switch and associated w/ VLAN, creating a logical barrier between end devices connected to the switch.
* This enables network administrators to create several VLANs on a single switch.
* **VLANs are logical, not physical, division**
* Transferring data betrween VLANs requires a router or other layer 3 devices.

## Benefits of using VLANs

1. **improved security**: VLANs help separate and isolate sensitive user data and reduce the chance of spreading malicious data and unauthorized user access via network traffic.
2. **Enhanced Performance**: VLANs reduce the size of broadcast domains, enhance performance, and minimize unnecessary traffic on the network.
3. **Simplified Management**: VLANs allow administrators to group end devices and users by departments (such as by job roles) rather than by phyiscal location. This improves network policy flexibility and reduces network costs.

## VLAN ID

* **what is a VLAN ID?**: When traffic passes through a VLAN, it must be identified to keep it separate from traffic in other VLANs. A unique ID identifies a VLAN in the network.
* There is complete separation between virtual networks, whereby users on VLAN 10 cannot access user data on VLAN 20.
* On cisco devices, the valid ID range for VLANs is 1 to 1005. There is also an additional extended range of valid VLAN IDs from 1006 to 4094.
* **The extended range of VLAN IDs from 1006 to 4094 is primarily used in large networks, such as an ISP network.

## VLAN Types
1. **Default VLAN**: VLANs 1 and 1002-1005 are reserved and added automatically during device installation. These VLANs cannot be removed or renamed.
2. **Data VLAN** VLANs 2-1001 are commonly used for data exchanges, their main function is to tag data traffic with an identifier. Its our day to day basic equipment plugged in, we could technically use any range we want besides the reserved ones.
3. **Voice VLAN**: This type of VLAN is designed for VoIP,(Voice over IP) network traffic. We use telephones as network devices now, they get typed into a telephone system, like their own servers and infastructures but they all communicate over the IP network, they get an IP address and all that.
4. **Management VLAN**: Interface VLAN 1 is a management VLAN used for SVI,a switch virtual interface.
* Management VLANs enable remote connection and conduct basic network functions.
5. **Native VLAN**: Native VLANs are designed to forward untagged traffic, such as DTP, Dynamic Trunking Protocol, and CDP, Cisco Discovery protocol, among switches. By default, VLAN 1 is a native and management VLAN.

## Default VLAN Settings

1. Command: Show vlan brief

* The command shows that the switch is already pre-configured w/ VLAN 1, and all ports are associated w/ it by default
* Additional VLANs are available in the switch configuration, they are reserved and known as default VLANs.

# Switchport Modes
* **the switch interface operates in one of two main modes: ACCESS or TRUNK**

1. **Access**: Access ports carry traffic only on the VLAN to which they belong, meaning it carries only on 1 VLAN. Access mode should only be defined on ports connected to end devices, such as PCs.
* As a security-related best practice, it is highly recommended to enable Access mode for a port before assigning to a VLAN.

2. **Trunk**: Trunk ports carry traffic for different VLANs and devices. The port set unique identifier **tags** on the ethernet frame, using either the 802.1Q or ISL, Inter-switch Link,encapsulation protocols. This ensures that each frame is directed to its intended VLAN. 

## VLAN Configuration

* **Command**: Vlan < id > 
* name < word >

* The example on the right shows VLAN 100 and 200 creation, whereby a valid ID is any number between 2 and 1001 ( 1,1002-1005 are occupied.) 
* It is recommended to assign an appropiate name to the VLAN upon creation.

1. S1(config)#vlan 100
2. S1(config-vlan)#name class_A
3. S1(config-vlan)#exit

1. S1(config)#vlan 200
2. S1(config-vlan)#name class_B
3. S1(config-vlan)#exit

## Interface Assignments

* **Commands**: switchport mode access
* swithport access vlan < id >

* The assignment of hosts (end devices, such as PCs) to different VLANs is done by matching the interconnected interface to the appropriate VLAN.
* **TIP**: Assigning mulitple ports to a VLAN simultaneously can be done using the range command.

1. S1(config)#interface range fastEthernet 0/1-2
2. S1(config-if)#switchport mode access
3. S1(config-if)#switchport access vlan 100
4. S1(config-if)#exit

1. S1(config)#interface range fastEthernet 0/3-4
2. S1(config-if)#switchport mode access
3. S1(config-if)#switchport access vlan 200
4. S1(config-if)#exit

## Verifying VLAN configuration

* **COMMAND**: Show vlan brief

* By running the show vlan brief, command it is easy to spot the two new VLANs and the interfaces assigned to them.
* To display the interface mode, use show interfaces switchport.

## Voice VLAN Configuration
* **COMMAND**: switchport voice vlan < id >

* Voice VLAN enable easier management of VoIP over the network.
* The example on the right shows how a Voice VLAN is set up on an interface.
* **NOTE**: VoIP settings on the network are necessary, but they are not within the scope of this course.

1. S1(config)#interface fastethernet 0/1
2. S1(config-if)#switchport mode access
3. S1(config-if)#switchport access vlan 100
4. S1(config-if)#switchport voice vlan 150
5. S1(config-if)#exit

# Trunk Protocol

1. **Trunking**: Trunk mode is designed to transmit multiple VLAN traffic sessions, over the same physical conncection, to a remote device, such as a switch or router.
* This is done by tagging frames w/ the source VLAN, ensuring that the Trunk link forwards the VLAN frames to the same VLAN on another switch. This helps maintain the isolation of other devices.

* **Trunk mode makes sure that relevant information stays among devices within the same VLAN(such as switches). However, routing among VLANs still requires a router.**

## Trunking Protocols

1. **ISL, Inter-Switch Link**: ISL is a proprietary protocol developed by Cisco that only operatoes on Cisco equipment, the protocol adds VLAN information to ethernet frames.
2. **IEEE 802.1Q**: 802.1q or dot1q is an industry standard developed by IEEE that allows trunk link creation between various vendor switches.
* Cisco uses this standard as its default trunk protocol, unline ISL, 802.1q encapsulates the VLAN info in the frame.

## Trunk Configuration
1. **COMMAND**: switchport mode trunk command sets the interface to trunk mode and creates trunk links.
* To display the trunks configuration, run the show interfaces trunk command.
* **NOTE**: the switchport mode trunk command creates a static trunk link, w/o using the DTP protocol. This is dynamic trunking protocol which does it automatically, it can negotiate the configuration and automatically configure it to be a trunk, most the time we want it to be atrunk link and DTP does that automatically.DTP has security concerns, any auto or enable by defualt we need to consider the risks, when its auto theres a possibility it can be missused or manipulated because theres no human oversight, DTP when switched on is able to be weak to rogue switches, and it can plug into another swithc, formulate a trunked link w/ a rogue switch. DTP we usually disable it, its on by default and this is why we have to disable because we must do it manually.

1. S1(config)#interface gigabitethernet 0/1
2. S1(config-if)#switchport mode trunk
3. S1(config-if)#exit

1. S2(config)#interface gigabitethernet 0/1
2. S2(config-if)#switchport mode trunk
3. S2(config-if)#exit

## DTP, Dynamic Trunking Protocol

1. DTP: a protocol developed by Cisco to automate the creation of trunk links, mainly to save time and prevent misconfiguration.
* DTP operatoes on Cisco switches by default and uses a special packet to "negotiate" the interconnected interfaces.
* DTP is also responsible for selecting the trunk protocol on both sides.
* **DTP can be disabled on specific ports for security purposes(such as to prevent switch spoofing attacks.)**

## DTP Modes
* **the protocol includes two port modes for interface ngotiation.

1. **Dynamic Auto**: This mode, which is the default for every port, is passive and does not negotiate. Instead, it waits until an explicit request is received from the other side and tehn establishes the trunk link.
2. **Dynamic Desirable**: This mode actively attempts to change the mode of the interconnected interface via DTP packets, to establish a trunk link, once a directly interconnected port is set to trunk, dynamic auto, or dynamic desirable, a link will be established.

## DTP Mode Configuration
1. **COMMAND**: switchport mode dynamic < mode >

* the example on the right shows the configuration of DTP modes on the interconnected interfaces of the switches.**remember**: Dynamic auto is the default mode.
* to display the interface mode, use show interfaces switchport.

1. S1(config)#interface gigabitethernet 0/1
2. S1(config-if)#switchport mode dynamic auto
3. S1(config-if)#exit

1. S1(config)#interface gigabitethernet 0/1
2. S1(config-if)#switchport mode dynamic desirable
3. S1(config-if)#exit

## Disabling DTP

1. **COMMAND**: switchport nonegotiate
* Since using DTP can make the switch vulnerable to a VLAN attack, it is best to disable DTP on a port connected to an end device.
* Configuring the port in access mode is not enough, and nonegotiate is required., to display the interface mode, use show interfaces switchport.
1. S1(config)#interface fastethernet 0/1
2. S1(config-if)#switchport mode access
3. S1(config-if)#switchport nonegotiate
4. S1(config-if)#exit

5. S1#show interfaces switchport

## Port Configuration Options

![Alt text](assets/port%20config.PNG)

## Native VLAN

1. **What is native VLAN?**: Native VLANs process untagged frames when they reach trunk ports. Untagged frames are frames that do not have a source or destination VLAN. VLAN 1 is the default native VLAN.
2. **Why is Native VLAN Required?**: W/o native VLANs, sending and receiving updatres for protocols such as CDP, VTP, DTP and STP among interconnected switches would not be possible, since trunk ports drop untagged frames.

## Important Native VLAN Points
* **Some essential points regarding native VLANS**
1. **Best Practice**: A best practice regarding native vlans is to re-assign them to non-default vlans, such as VLAN 200, for security purposes, doing so can for example mitigate double tagging attacks
2. **Identical NAtive VLAN**: The same native VLAN must be used on both ends of the trunk link, if not untagged frames will not be delivered correctly, and the switch's OS will continuously send warning messages to the user, in the form of: %CDP-4-NATIVE_VLAN_MISMATCH: NAtive VLAN mismatch discovered on gigabitethernet0/1(200), w/ S2 Gigabitetherenet0/1(1)

## Native VLAN Configuration

1. **COMMAND**: switchport trunk native vlan < id >
* the example on the right shows how to change the defualt native VLAN on two interconnected switches, to display the native vlan setting use show interfaces trunk.

1. S1(config)#interface gigabitethernet 0/1
2. S1(config-if)#switchport trunk native vlan 200
3. S1(config-if)#exit

1. S2(config)#interface gigabitethernet 0/1
2. S2(config-if)#switchport trunk native vlan 200
3. S2(config-if)#exit


**By default the trunk carries all VLANS, whatever is configured, will converse the trunk**

# Inter-VLAN Routing

## Inter-VLAN Routing Overview

1. **Inter-Vlan Routing**: Although VLANs are logical segments, they still oeprate within the framework of a network, which means they are also broadcast domains.
* switches(which generally operates at layer 2) cannot move traffic across different VLANs or broadcast domains.
* Routing data among different VLANs requires a layer 3 device (such as a router) which encapsulates and decapsulates the frame.
* **A layer 3 switch ( also known as a multilayer switch) can be used for routing among VLANs which can also reduce the amount of network components needed to handle the traffic.**

## Router-on-a-stick

* Intervlan routing works: The most common technique for intervlan routing is called router on a stick. 
* this method is effective because it requires only a single physical connection between the switch and hte router, avoiding the need for additional componenets and costs.

## Sub-Interface

1. **Multiple IP Addresses**: Multiple IP addresses are possible because a routers single physical interface is segmented itno multiple logical interfaces, called sub-interfaces.
2. **Logical interface**: Each sub-interface is configured w/ a unique IP address and subnet mask. Every sub-interface represents a default gateway for a specific VLAN.

**Simple Rule: The number of VLANs dictate the number of sub-interfaces.**

* SUB-INTERFACE COMMAND: R1(config)#interface gig 0/0.1
1. R1(config)#interface gig 0/0.2
2. R1(config)#interface gig 0/0.3

## The Switch Side

1. **COMMAND**: Switchport mode trunk

* Enabling Trunk 

1. S1(config)#interface gig 0/1
2. S1(config-if)#switchport mode trunk
3. S1(config-if)#exit

* on the switch side, set the local interface connected to the rouyter to trunk mode, this enables VLAN tagging towards the switch.

## Inter_VLAN Routing Configuration

1. R1(config)#int gig 0/0
2. R1(config-if)#no shutdown
3. R1(config-if)#exit

1. R1(config)#int gig0/0.1
2. R1(config-subif)#encapsulation dot1q 100
3. R1(config-subif)#ip address 10.0.0.1 255.0.0.0
4. R1(config-subif)#exit

1. R1(config)#int gig0/0.2
2. R1(config-subif)#encapsulation dot1q 200
3. R1(config-subif)#ip address 192.168.0.1 255.0.0.0
4. R1(config-subif)#exit

1. On the router side, enter the physical interface and enable it
2. Create a sub-interface
3. Configure interface encapsulation on 802.1Q and assign the appropriate VLAN ID.
4. Configure the VLANs corresponding IP and mask (default gateway)
5. Repeat this process for every VLAN.

## Verify Configuration

R1#show ip interface brief

* Use show ip interface brief to display the interface settings and mode.
* The show running-config command shows additional details, such as the interface and its VLAN ID.