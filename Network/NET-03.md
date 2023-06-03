# Switch & IOS Fundamentals

## Table of Contents
1. Switch Fundamentals
2. The Cisco IOS
3. Initial Device Configuration
4. Managing IOS & System Files

# Switch Fundamentals

## The Switch
* Switches are smart Layer 2 devices w/ many ports designed to forward frames from source to destination, according to specific MAC addresses in the frame ( Data-Link Layer)
* They include multiple technologies providing various capabilities
* Switches were developed to forward frames in accordance w/ their destination addresses and MAC tables using MAC learning process known as forwarding decision.
* The switch is to keep track of all the nodes in a LAN
* Switches receive **ethernet frame** and it has 3 methods to rely the data
 this is our **switching methods**
## MAC Tables

* The command used to display the MAC address table is **show mac address-table**
* Mac Address tables include the following columns
1. VLAN
2. MAC address
3. Dynamic or static
4. Associated physical ports

* **DYNAMIC**: refers to a frame w/ a source MAC that arrives at a switch and updates the table w/ the MAC address for that port.
* **STATIC**: indicates a manually configured MAC address on a switch.

* **NODES** are a resource on a network
## Switching Methods
* Switches have different methods of receiving and transmitting frames on the LAN. 
* The following switching methods are used:
1. Store-and-forward
2. Cut-through
3. Fragment-free

## Store-and-Forward Switching

* A switch using the store-and-forward method buffers the entire frame upon receipt. This enables the switch to support various port speeds. For example, a frame received on a 100 mbps ingress port can be transmitted via a 1 gbps egress port.
* Another advantage of this method is error checking, which can be done once the entire frame is buffered, this is the #1 advantage **is error checking** but to know the error checking you'd need the entire frame. The Switch can easily detect frame errors using the FCS field.
* Although store-and-forward is relatively slow, it does provide error checking and support for different speeds across multiple ports, **this is the slowest method, but offers error checking**
## Cut-through Switching
* Cut-through is the default for cisco switches, which is the fastest
* Cut-through switching is a much faster method than store-and-forward, in this method, only the first 6 bytes of the incoming frame are buffered, meaning the switch only regards the destination MAC address of the frame.
* The switch forwards the frame immediately, even before checking the entire frame is received, and no error checking is done, **note**: Modern switches can buffer up to 14 bytes of the beginning of a frame, before deciding what to do with it.
* Although the advantage of cut-through switching is its speed, a significant disadvantage is that most frames that reach the destination host are corrupted due to lack of error checking.
## Fragment-Free Switching
* Fragment-free switching is a more advanced method.
* This method buffers the first 64 bytes of the frame, including MAC address data and the frames payload. The technique provides faster switching than the store-and-forward method while also performing partial error checking to make sure there is no fragmentation on the first 64 bytes of the frame.
* Fragment-free switching is therefore a better choice, as it is faster than store-and-forward switching and provides partial error cehcking, unlike the cut-through method

* **how come there are error checkings that happen?** This can happen when we are transmitting data physically, there can be some incorrect interpations of 1's or 0's and that can make the data become corrupt.
* Fragment-free does partial error checking
## Duplex Operation
* **Half-Duplex**: a connection for which the communication is restricted to exchanging data in one direction at a time. For example, a walkie-talkie is a half-duplex device because only one person at a time can talk.**usually legacy devices**
* **Full-Duplex**: Full-duplex means that data can be transmitted in both directions, on a signal carrier, at the same time. Ex. a telephone is a full-duplex device because both users can talk at once.**most modern devices use full-duplex**
## Port Speed
* **Switch Ports**: Switch ports can transfer traffic at speeds of 10 mbps, 100 mbps, or 1000 mbps.
* The default is for the switch port to auto-configure its speed based on signaling between the port and the connected device.
* **There are switches that can transfer traffic at 10 gbps or even 40 gbps.**
* Jumbo frames: are frames that are bigger than 1500 bytes, meaning that the equipment must be able to transmit and handle the larger amount of packets of data.
## Auto-Negotiation

* Auto-negotiation tells connected devices to annouce their capabilities, and then, based on the settings of the interconnected device at the other end, chooses the optimal speed and duplex mode.
* **if one of the devices is configured with a different mode, a duplex mismatch will occur.**
* This is auto configuration that the switch will automatically choose the correct duplex.

# The Cisco IOS
* Every network device, such as a switch or router, has an operatin system that tells it how to forward packets and execute network operations.
* A operating system for a devbice known as a Network Operating System ( NOS)
* An NOS does not operate in the same way as PC and server operating systems.
* An internetwork operating system ( IOS) is a command line interface (CLI)-based system, and users interface with it using text-based Cisco commands.
* Most Cisco devices, regardless of their size or type, run the IOS, which is an advantage due to singularity and familiartiy
* While alldevices come with a default IOS and feature set, it is possible to upgrade the IOS version or feature set to obtain additional capabilities, this course focuses on versions 12 and 15
## IOS Interface Features
* **Command Line**: IOS uses a command line interface (CLI) to enable administrators and technicians to interact w/ the system via special cisco commands. 
* **CLI**: CLI is a means of interacting w/ programs by entering commands on a command line. Using a CLI-based system has many advantages, such as minimum resource usage, faster ability to operate on the system, and others.
* **Terminal Emulation**: Many network devices are configured and managed using Terminal Emulation (TE) software, such as PuTTTY, TE programs enable configuration of local devices using a serial cable or a remote management protocol, such as SSH
## Terminal Software

* **PuTTTY**: is a versatile tool for remote access to another computer, it is often used by people who want to secure remote shell access to a UNIX or Linux system, though that is only one of its many uses.
* **Tera Term**: Tera Term is an open-source, free, software-based terminal emulator ( communication ) program. It emulates different types of computer terminals, from DEC VT100 to DEV VT382, and supports Telnet, SSH 1 and 2, and serial port connections.
* **SecureCRT**: SecureCRT is a commercial SSH and Telnet client and terminal emulator by VanDyke software, originally a windows product, VanDyke recently added Mac OS X and linux versions.
## Cisco Packet Tracer
* Cisco Packet Tracer allows the user to map a network, Packet Tracer enables the testing of network configurations, trains users to work w/ network configuration, helps them understand how a network operatoes, and provides them w/ network deployment dexperience.
## Access Methods
* **Out-of-Band**: This method uses a dedicated management console cable that must be phyiscally connected to the device, Initial configuration is usually done using this method. This could be connecting to the network out of base, using something physical, like a cable

* **In-Band**: This method uses management protocols, such as SSH, or Telnet, which access the device remotely over the network
* when we hear band, think of in the network, apart of the network, inband means we are in the network

## Out-of-Band Management
* Out of band management requires two main items
1. PC w/ terminal software
2. Console Cable

* **Terminal**: A network device is like a PC, but w/o a mouse, keyboard, and screen. A PC w/ a terminal provides a way to input commands and view output from the device.
* **Console Cable**: A console cable or management cable is like a bridge between the PC and the device. Almost every device has a designated console cable for this purpose. Older cables use an RS-232 connector; modern ones use USB. A DV9 cable is another one. The console has a rj-45 connector that is plugged into the cisco switch, it works only for the console port.

## IOS Modes
* **Permissions**: IOS can operate in one of three work modes, each w/ different capabilities and permissions, for ex. one mode may have a lower level of privileges compared w/ another mode.
* **Modes**: The division of modes is meant to separate the management levels and increase the efficiency of network device security and configuration.
* **Structure**: Cisco IOS modes have a hierarchical strcuture and are similar among switches and routers.

* **User EXEC Mode**: This mode has low-level capabilites but is useful for basic operations, it has a limited number of monitoring commands and does not allow device configuration changes. = Switch
* **Privileged EXEC Mode**: This mode has a larger number of monitoring commands and device configuration viewing commands (show commands). It also enables file management operations, such as device configuration backups and IOS upgrades.
* **Global Configuration Mode**: Global configuration is the only mode that allows administrators to change device configuration. This mode is only accessible from the privileged EXEC mode.= name(config)# 
* **Interface Configuration Mode**: The interface mode allows you to cahnge specific parameters within a switch or router. = name(config-if)
* **Navigating IOS Modes**: Navigating the system and understanding the difference between the modes is very important when working in the system
* The default display name of a device appears before the prompt. In ex. a name could be "switch"
* The **enable** command moves the user from user mode to privileged mode.
* The **configure terminal** command moves the user from user mode to global configuration mode.
* the **Exit** command takes the user one mode back.

## Cisco Device Components

* **RAM**: Volatile memory that stores the system configuration (running-config) and tables (such as the MAC table)
* **ROM**: Non-volatile memory responsible for the Power-On Self-Test(POST) process and bootstrap, which is the initial program responsible for booting the IOS.
* **FLASH**: Non-volatile memory that stores the operating system itself (IOS).
* **NVRAM**: Non-volatile memory that stores the startup config file. Non-volatile random access memory

## Device Boot Process
* **POST**: POST and bootstrap program load: this part of the sequence checks the CPU, RAM, and NVRAM. When done, the device copies the bootstrap program from the ROM to the RAM, **Loads IOS**: After copying the bootstrap program from the ROM to the RAM, the IOS (which is still stored in flash memory) is copied to the RAM for execution. **Load configuration**: The bootstrap program now copies the startup configuration file from NVRAM to the RAM.
# Inital Device Configuration

## Device Name
* **Command**: -
hostname < device name >
**Set Device NAme**
Switch(config)#hostname S1-Floor1
S1-Floor1(config)#
* **sets the local network device name; for ex. S-Floor1
## Create User-Account
* **Command**: - username < user-name > password < password >
* **create account**: - Switch(config)#username Admin password p@nd@
* Switch(config)#username Peter password Spiderm@n
* **creates a local user account on the device**
## Secure Privileged Mode
* **command**: - enable password < password >
* **Set Password**: 
Switch(config)#enable password c!sc0
* **enables password authentication when accessing the privileged EXEC Mode.
## Security Message
* **Command**: - banner motd #security-message#
* **set Message**:
* Switch(config)#banner motd #Access to this device is for authrized personnel only!#

Press RETURN to get started!

Access to this device is for authrized personnel only

User Access Verification

Password:

* **Displays a security message each time a user logs in to the system.**

## Encrypt Passwords
* **command**: - service password-encryption
* **encrypt passwords**:
* Switch(config)#service password-encryption

* **Configured passwords appear in plain text in the configuration file. This command encrypts all plain-text passwords using the Cisco Type 7 method.**
## Save Device Configuration
* **command**: - copy running-config startup-config
* **save configuration**: 
* Switch#copy running-config startup-config
* **copies the device configuration from the RAM to the NVRAM (non-volatile memory) if the configuration isn't saved to the NVRAM, all configurations that were performed will be lost.**
## Secure Console Access
* **Command**: - line console 0 & login local
* **Secure Console Port**:
* Switch(config)#line console 0
* Switch(config-line)#login local
* Switch(config0line)#exit
* Two steps are performed to enable local credential ( username and passsword) authentication on console port.
1. Enter the console port config mode (line mode).
2. Enter the local login and exit.
* **note**: Besides the local login command, there is a login command that enables only password checking.
## Verify Configuration
* all configuration cahnges are immediately saved in the **running-config** file.
* To display them, run the **Show running-config** or **Show run** command.
