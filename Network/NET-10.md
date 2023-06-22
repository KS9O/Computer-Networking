# Diagnostics & Troubleshooting

## Table of Contents
1. Troubleshooting Methods
2. Neighbor Discovery Protocols
3. Log Events & Syslog Server
4. Network Time Protocol 

# Troubleshooting Methods

* Issues can and will arise, even in networks that were designed using the most advanced technologies.
* This lesson covers the ways network issues can be solved and the tools that can help resolve them quickly and efficiently.
* An important aspect of network troubleshooting, also described in this lesson, is the usage of discovery protocols.

## Troubleshooting

* **Documentation**: A quick and efficient troubleshooting is based, in part, on continuous and detailed network-related documentation.
* **What does documentation include?**: Network documentation includes the following: physical and logical topological diagrams, network and end-device backup configuration files, IP and MAC addressing schemes, and network performance baselines.

* In networking there are 2 different types of drawing, physical topology, think 

* physical layer; switches, routers, it shows us how the physical components are connected, where the cables go, why type of cable, what they are connected to, what type of cable is it? think layer 1.

* Logical topology, think layer 3 information, this is our drawings of subnets, ip addresses, shows how data moves between subnets, ip addresses, interfaces

## Troubleshooting Steps
![Alt text](<assets/Troubleshoot steps.PNG>)

![Alt text](<assets/Gathering Info.PNG>)

* OSINT, Open Source intelligence, its a fancy way of saying all the information on the internet. go to the internet

* we have to be mindful we aren't jumping to solutions or probable cause, we should gather as much information as possible, we should hold off on jumping to conclusions and allow it to come from experience, so investigate and gather info, going slow, thinking through the process and asking right questions.
## Open Systems Interconnection (OSI) Troubleshooting Methods

![Alt text](<assets/OSI troubleshoot methods.PNG>)

## Software Tools
* **Software Tools**: Network Management Software (NMS) provides excellent tools for troubleshooting.
* NMS continusously monitors network activity and establishes a clear baseline for reference purposes. This enables network administrators to promptly identify issues, and, in some cases, even predict the occurrence of such issues.

## Top IOS Show Commands

![Alt text](<assets/TOP IOS show commands.PNG>)

## Extended Ping & traceroute Commands

* **Extended Ping**: extended ping is used to perform advanced checks of network connectivity. It is also able to change the source IP on the packet leaving the router.
* **Traceroute**: the traceroute command discovers the path packets take to a remote destiniation and where routing failures occur.

# Neighbor Discovery Protocols

* **Cisco Discovery Protocol , CDP**: CDP ( Cisco Discovery Protocol) is a layer 2 cisco proprietary protocol enabled by default on all cisco devices. Its purpose is similar to the purpose of NDP.
* CDP can be disabled on specific devices or interfaces for security reasons.
* It allows us to quarry, see information about connected devices. If we didnt have access to a topology but we did have access to a router, we could tell the router to show us its neighboring devices and it would reveal whats connected/near by the router, and we could use that to learn about the topology. **We do disable, as it is enabled by default.**

## CDP Characteristics

* **Eavesdropping**: Since CDP does not encrypt transmitted data, it is vulnerable to reconnaissance-type attacks ( such as sniffing) Such attacks will allow the attacker sto map the victims network and more.
* **Information Gathering**: CDP gathers information on the local device and periodically sends it to all directly connected devices.
* **Advertisements**: CDP advertisements are special packets that reveal device details to neighbors also running CDP. When advertisements are received, they are stored in the neighbor table.

## CDP Advertisement

![Alt text](<assets/CDP advertisement.PNG>)

## Mismatch Detection

![Alt text](<assets/mismatch detection.PNG>)

## CDP Intervals

* CDP Packet Timer: CDP Sends advertisement packets every 60 seconds by default to all directly connected devices.
* CDP Holder Timer: If a device doesn't receive CDP packets from a neighbor for 180 seconds, it will consider that neighbor "dead" and remove it from its neighbor table.

**The timers can be modified**

## CDP Configuration

1. Command: cdp run \ enable
* Enable/disable on device
1. S1(config)#cdp run
2. S1(config)#no cdp run
* enable/disable on port
1. S1(config)#int range fa0/1-24
2. S1(config-if-range)#cdp enable
3. S1(config-if-range)#no cdp enable

* Because cdp is not secure or encrypted, it is easy to eavesdrop, if necessary, the protocol can be turned off entirely on the device or on selected interfaces. 
* Recommened: Enable CDP only for port interconnection w/ other networks

## CDP Usage

* **show cdp neighbors**
* **show cdp neighbors details**

## LLDP, ( Link Layer Discovery Protocol)

* LLDP is a neighbor discovery protocol similar to CDP that was developed by the IEEE.
* LLDP is an industry standard protocol, meaning it is not proprietary and can operate on any network device, and even on PCs and servers.
* Although LLDP is not enabled by default on cisco devices, it is fully supported.

## LLDP Intervals

![Alt text](<assets/LLDP Intervals.PNG>)

## LLDP Configuration

![Alt text](<assets/LLDP Configuration.PNG>)

# Log Events & Syslog Server

* **What is a syslog?**: Syslog is a standard for logging messages of each device's records actions and events that occur like a private diary.
* Among other tasks, network administrators need to monitor the network to ensure smooth, errorless functionality.
* Monitoring the network improves troubleshooting capability and helps identify issues such as device health and network load.
* **The syslog protocol is documented in RFC 5424**

## System Log Events

* **Why are Logs useful?**: System notification logging increases a network administrator's awareness of hardware or software malfunctions, service status, and security accountability.
* In some cases, logs can be used to predict component failures.

* Log analysis can help administrators troubleshoot the system and can be useful to information security experts when investigating security breaches.
* **Syslog messages can be stored locally on the device or on a syslog server in the network.**

## Device Logs

* **Log Storage**: Log storage takes up space, and can, in some cases, degrade system performance.
* Log message count is limited due to buffer size
* Collecting logs from separate devices can take a long time
* RAM is erased upon device power off.

## Syslog Storage Methods

* **Logging Buffer**: A logging buffer is a predetermined storage space allocated on RAM for syslog messages

* **Console Line**: Console Line is a method of viewing messages locally via the console window
* **Terminal Line**: Terminal line is a method of viewing messages via a CLI program(such as PuTTy)
* **Syslog Server**: If a syslog server is configured on the device, the device will send all syslog messages to the server over the UDP 514 port.

## Syslog Server

* **A Syslog Server?**: a syslog server is a computer that runs syslog software, the syslog software concetrates logs from all devices (PC, router, Etc.) on the network into one centralized location, which makes management and log backup easier.
* It also offers a convenient user interface, this way of working is more efficient than storing logs in RAM
* **Many free and enterprise versions of syslog exist, such as the kiwi syslog viewer.**

## Severity & Facility
* **Syslog messages include several pieces of information, of which the most important are:**

* **Message Severity**: The urgency of the log message is represented by its severity level, which is a number value from 0 to 7. Level 0 indicates emergencies, and 7 indicates system debugging. The values also represent critical malfunctions and system warnings.
* **Message Facility**: The facility paramter indicates the source that generated the message, which, for example, can be a network card or routing protocol. The facility can be a hardware component, protocol, or system service.

## Syslog Message Severity Levels

![Alt text](<assets/Sys Log Message Severity.PNG>)

## Log Message Format

![Alt text](<assets/Log Message Format.PNG>)

## Syslog Configuration Commands
* **Typical confiruation commands used to set up syslog on a cisco device**

![Alt text](<assets/cisco config commands.PNG>)

## Syslog Config Example

![Alt text](<assets/Sys Log Message Severity.PNG>)

## Network Time Protocol

The useful ness of our logs is important for the time we visit it, the the clocks on all the systems different, it would make correlating events very very difficult, or ability to reconstruct all the events that transpired to have accurate time of when it all happened on the systems, our systems need to be all on the same time.

## NTP

* NTP(Network Time Protocol) is responsible for the synchronization of the time and date acrros all devices on the network.
* NTP is a simple client-server protocol and is implemented in networks everywhere.
* It is very easy to set up and even has an authentication mechanism for security.

* **NTP operatoes on UDP port 123 and is defined in RFC 1305.**

## Time Configuration
* **Date and time for network devices can be set in one of two ways**
* **Manual Configuration**: This method regquires manual setting of the time and date on each device on the network. It is not recommened to work this way for various reasons, among which is the lack of scalability for large networks. ( Setting the clock in every device will waste valuable time.)

* **Automatic Configuration**: This method requires an available and configured NTP server.
* Only the server's IP address needs to be set on network devices.
* This ensures that all devices on the network will be set to the most accurate time and date automatically
* Cisco routers can be configured to act as NTP servers.

## NTP Operation

* **NTP Usuage**: Cisco routers and switches ( and many other devices around the world) use NTP to determine the date and time, although routers and switches can also act as NTP servers.
* **Stratum Model**: Stratum levels define the distance from high-precision reference clocks, which begin with stratum 0, to devices connected hierarchically. Servers linked to the reference clock are stratum 1, devices that receive the time from the servers are stratum 2, and so on. To avoid delays, a maxium of 15 levels are allowed.
* **Services**: Accurate time settings are crucial for many protocols and device functions. For example, DHCP leases and syslog events are time-sensitive services. Timestamps are extremely important for troubleshooting, management, and network security.

## Manual Time/Date Setting

1. COMMAND: clock set < hh:mm:ss > < day> < month-name > < year >

1. R1#clock set 09:21:14 16 January 2019

* **Setting the clock manually has two drawbacks: a device can get out of sync if it is shut down, and setting every device clock can waste valuable time.**

## NTP Configuration

![Alt text](<assets/NTP Configuration.PNG>)

## NTP Master
1. COMMAND: ntp master < 1-15 >

1. R1(config)#ntp master
2. R1(config)#do show run ntp

* **A network device such as a router or switch can act as an NTP server, the main command requires only a stratum value and the number of hops from an accurate time source ( such as an atomic clock)**

