# Switch Security

## Tables of Content
1. Port Security
2. Remote Access

# Port Security
## Risks in a Switched Environment

* **MAC Spoofing**: MAC spoofing is when attackers change their physical PC address to conceal their true identity and pose as someone else. Ex. an attacker can spoof a MAC address w/ a legitimate MAC address to bypass an access control mechanism such as port security. (There is software that can change via drivers etc. to change our MAC address)

**spoofing should be thought of as "pretending" "faking"**
* **CAM Table Overflow**: Content Addressible Memory, CAM table overflow is an attack that targets a switchs MAC table. The aim is to flood the table w/ a large number of fake addresses. When the list of addresses exceeds the maximum size of the table, the switch will initiate its fallback mode and begin to act as a hub. This means that every frame will be forwarded to every host on the network. This is to evasdrop on the network through the switch because it can no longer segregate communications. 

## Port Security
* **Overview**: The port security feature is used to restrict input to an interface by limiting access to a specific port to selected MAC addresse of workstations. When secure MAC addresses are assigned to a port, the port will not forward packets w/ source addresses outside the defined group.
**by default, port security is not defined on switches and requires configuration**

## Violation Modes

* **shutdown**: This is the default violation mode, when a violation occurs, the port will be shut down and logged out automatically. The port must then be reset manually to become opertional again.

* **restrict**: In Case of a violation, ethernet frames w/ unauthroized source MAC addresses will be dropped. The switch provides notification of security violations and keeps count of the nukmber of violations. It can recover itself automatically, doesn't require a Admin, once the MAC is returned, it auto recovers.

* **protect**: In case of a violation, ethernet frames w/ unaothroized MAC addresses will be dropped. In this violation mode, the switch does not provide notification regarding the event.

**the port security feature includes three protection modes to handle incidents in which it receives an ethernet frame w/ a restricited MAC Address**

## Manual vs. Sticky
**MAC address learning can be performed in one of two ways: Manual or sticky.**

* **Manual**: The manual method requires static configuration of each allow MAC address and its assignment to an interface. This is the most secure method, but it is very time-consuming and open to faulty configuration.

* **Sticky**: In the sticky method, allow MAC addresses are learned dynamically and limited to the maximum number configured for the interface. The switch learns the source address of the first few devices associated w/ the interface, providing a fast and scalable method of operation.

## Max and Err-Disabled

* **Maximum Allowed MAC Addresses**: Although the default number of allowed MAC addresses in port security is one, the number can be changed within the range of 1 to 3072.

* **Err-Disabled**: When a switch port is in err-disabled mode, the port may have been disabled automatically by the switch operating system due to a port security shutdown mode violation. we can check this with the command, **Switch# show interfaces [interface-id] status** this is happens when the switch disables it because of an error.

## Common Triggers for Err-Disabled

* **Duplex Mismatch**: This state occurs when wo parties set for point-to-point communcation are configured to use dfifferent duplex modes.
* **Bad NIC**: Faulty card w/ software or hardware issuses
* **Broadcast Storms**: When a broadcast volume is too large for processing in the broadcast domain, the switches may become overhwelmed and trigger err-disabled mode on their ports.

## Port Security Requirements

* Access ports are responsible for traffic flow.
* Access mode should be defined only on ports connected to end point devices, such as PCs.
* You can configure port security on interfaces that you coifngiured as access ports w/ access mode.

## Enable Port Security

* Switch(Config)# interface fastEthernet 0/1
* Switch(config-if)# switchport mode access
* Switch(config-if)# switchport port-security

## Port Security Configuration

From above we contiune with
* Switch(config-if)# switch port-security violation restrict
* Switch(config-if)# switch port-security mac-address sticky
* Switch(config-if)# switch port-security maximum 5

* this is a sticky method where it will be seen, if a 6th mac is tried to open, it will cause a violation.

## Port Security Show Commands

* Switch# Show port-security
* switch# show port-security address, this reveals all the learned MAC addresses.

## More Commands
* switch(config-if)# shutdown
shutdown | no shutdown
interface range

# Remote Access

## Telnet vs. SSH

**Telnet and SSH are the two most widely used command-line interface (CLI)-based remote access protocols
* **Telnet**: Telnet was developed many years ago to enable users to manage devices from anywhere, via asimple and minimal configuration. However, using telnet involes a potential security risk because usernames and passwords are sent in plain text on **TCP port 23.**

* **SSH**: SSH is similar to telnet, but it has a significant difference: SSH encrypts all data transferred between the user and end device. SSH uses RSA encryption, a robust and reliable encryption, it operates on **TCP Port 22.**

## SSH Encryption

* **RSA Encryption**: Modern encryption relies heavily on the RSA algorithm because most methods use public and private encryption keys.
* The public and private encryption key method, also known as asymmetric cryptography, uses two different but mathematically linked keys
* The public key is shared w/ everyone, whereas the private key is given only to specific persons.
* RSA ensures the confidentiality of the CIA triad and avoids authentication rejection.
* Protocols such as SSH and SSL/TLS use RSA to encrypt communciation and digital signatures.
* RSA depends on a powerful computational system, the more complicated the keys are, the more power is required.

## Asymmetric Encryption

* Asymmetric encryption is when two different keys are used to encrypt and decrypt messages. The keys are mathematically related in a way that messages encrypted w/ one key, typically the public key, cannot be decrypted by it.

* Decryption can be done only w/ the corresponding private key in the key pair. This method is considered more complex and slower than symmetric encryption, which uses one key for both encryption and decryption.

## Virtual Teletype (VTY)

* **VTY**: VTY is a CLI in network devices used to create remote-access connections, VTY is virtual and doesnt require any hardware.
**switches have 16 VTY lines (0-15). Routers have five VTY lines(0-4)**

## Switched Virtual Interface (SVI)
* The primary purpose of creating a computer network is to share resources and enable communication within the network, Layer 2 switches create virutal LANs (VLANs) that form a single croadcast domain. If a broadcast message is sent within the same VLAN, all devices connected to that VLAN will receive the message. Host can communicate on the same VLAN w/o a Layer 3 device(router). However, devices on a different VLAN cannont communicate w/ each other w/o proper routing.
* A router or Layer 3 switch can handle network segmentation and inter-VLAN communication, a router can segment a network and create a separate broadcast domain, each network segment uses a different sub-interface of a physical interface on the router.
* Layer 3 switches require the creation of multiple VLANs on the switch, which form multiple croadcast domains, then, for each VLAN, a corresponding layer 3 interface needs to be created on the switch to handle the routing, this layer 3 interface is the SVI.
* The difference is that SVI layer 3 interface is virtual.

## SSH Configuration

![Alt text](assets/SSH%20Configuration.PNG)

* at 6, we disable telnet
* at 7, SVI

## SSH Prerequisites

1. switch(config)#hostname 
2. [hostname](config)#username admin password [password]
3. i have all thes ecommands this is the new one
4. s1(config)#ip domain-name CyberPro.com

## Allow Remote Access
* S1(config)#line vty 0 15
* S1(config-line)#login local
* S1(config-line)#transport input ssh = only uses SSH, makes only SSH viable
* S1(config-line)#exit

## IP Switch Settings

* Commands: interface Vlan 1
* Commands: ip address <ip-address> <subnet-mask>

## Generate RSA Keys

* Command: crypto key generate rsa
## Verify SSH Configuration
* Command: S1#show ssh
* command: S1#show ip ssh

## SSH Connection

* Accessing the device remotely w/ SSH can be done by using a CLI, such as PuTTY, or a device terminal
* The universal command for creating an SSH session is *ssh -l < username > < target-ip >, its a lowercase ' l ' as in Liana


