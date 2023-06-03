# Network Fundamentals

## Table of Contents
1. Network Protocols & Models
2. OSI Models
3. TCP/IP Model
4. Transport Protocol and Logical Ports
5. Introduction to Wireshark Addresses
6. ARP & Encapsulation

# Network Protocols & Models

## Client-Server

* **Client**: A client represents the endpoint device (not necassarily a PC) that requested an operation.
* **Server**: A server represents the endpoint device that receives a request and performs the requested operation.
* **Web Browsing**: Client speaks to server saying "please take me to (IP) 182.43.12.09 to see facebook page", and server receives request (IP) 182.43.12.09 and brings client to facebook page.

* **Client-Server Relationship**: The client-server model is a distributed application structure that manages tasks and workloads by sharimg them among providers of resources and services (servers) and delievers responses to service requesters (clients).
* **an alternative method is to use broadcast or multicast channels to distribute information.

## Common Network Protocols
* **HTTP**: Http is an unsecure proctocol used to transfer information over the web. Because HTTP traffic is not encrypted, it can be sniffed on the network, ex. if credit card info is entered in an HTTP website, it can be captured in simple text format.
* **HTTPS**: HTTPS is the encrypted version of HTTP. It is used for secure communication and is widely used on the internet, communcation is encrypted using TLS (Transport Layer Security) or SSL (Secure Socket Layer)
* **DNS**: DNS translates domain names to IP addresses according to predefined databases. The DNS protocol is used for address resolution in a network, ex. when a URL is entered in a browser, the DNS protocol translates the domain that was entered to an IP address.
* **FTP**: File Transfer protocol is used to transfer files over the network, ex. FTP service can be used to transfer files to another device over the network.
* **DHCP**: Dynamic Host Coniguration Protocol, is rsponsible for assigning an IP adress to each device on a network configured to use DHCP, such as PCs, Routers, Firewalls, Servers, etc. Ex. a PC configured with DHCP will automatically be assigned an IP address upon startup.
* **SMTP**: Simple Mail Transfer Protocol is the standard protcol for mail transfer over the internet. Ex. when a email is sent over the network, the SMTP manages the operation.
* **SSH**: Secure Shell is a secure command line proctocl that allows the user to run remote commands on a remote machine, any data that passes through SSH is encrypted, ex. when a remote connection is made to a device the connection is made using SSH on port 22.
* **ICMP**: Internet Control Message Protocol is used by network devices to generate error messages when IP packets are not able to reach their destinations.

## Network Models

* **Network Model Concept**: The idea behind creating a networking model was to set a standard for the development and usage of network components, Standards allow devices to communicate without requiring continuous configuration in different device platforms, in addition, diving the networking process into smaller sub-proceses helps debug issues and pinpoint solutions.
**TCP/IP and OSI were developed around the same time with the aim of solving the same problem.**

## OSI vs. TCP/IP
* **today, OSI and TCP/IP are very similar due to the way they evolved over time. OSI is often used as an education model, while TCP/IP is used more as a practical model.**

* **OSI**: OSI is a network model in which each functionality of the network is represented by a layer, there are seven layers, and the functionality of each is dependent on the one below it, OSI was developed by the International Organization of Standardization.

* **TCP/IP**: the first TCP/IP specification was submitted several years after the OSI model. The original TCP/IP model consisted of four layers but was later updated to the current five layers. However, the four-layer version is still more commonly used, TCP/IP is used for network analysis, due to its lesser invovlement with the top three layers.

# OSI MODEL

## Open System Interconnection ( OSI )

* OSI defines a networking framework to implement protcols in layers.
* OSI conceptually divides computer network architecture into a logical seven-layer progression.
* Lower layer deals with electrical signals, chunks of binary data, and routing data across networks.
* Higher levels cover network requests and responses, data representations, and network protocols, from a user's viewpoint.


* The OSI model is divided into seven layers,
1. Application
2. Presentation
3. Session
4. Transport
5. Network
6. Data Link
7. Physical
* when the network traffic is generated, it is assembled (encapsulated) from the top layer to the bottom layer.
* When received, traffic goes through the model in reverse direction, from bottom to top ( decapsulated )

## Upper Layers

* **Layer 7: Application**: Users interact direvtly with the applications that operate at Layer 7, Ex. Layer 7 applications include web browsers, and other applications, such as SSH and FTP.
* **Layer 6: Presentation**: This layer prepares or translates data from application format to network format, and vice versa, Ex. the presentation layer operation is the encryption and decryption process.
* **Layer 5: Session**: The session layer is responsible for creating a session between two devices, it is also responsible for session checkpoints and recovery.

* **UPPER LAYERS**
7. Application
6. Presentation
5. Session

* **Layer 4: Transport**: Transport layer handles coordination of data transfer between end systems and hosts, including how much data to send, at what rate, destination, etc. Data in this layer is organized into segments. The transport layer determines if the connection should be instantiated, how to verify data integrity, how to recover from a connection error, and if retransmission is necessary, the protocols in this layer provide flow control, multiplexing, and reliability.
* **TCP and UDP are discussed in more detail in later slides.**
* **Layer 3: Network**: Network layer organizes data into packets called IP datagrams that contain logical source and destination addresses. Routers operate in this layer, the network layers job is to allow hosts to send packets across multiple paths to any other network and deliver them to their destinations, via routers operating on this layer. **Diagnostic tools such as ping and tracert operate in this layer**
## Lower Layers

* **Layer 2: Data Link**: The data link layer provides node-to-node data transfer (between two directly connected nodes) and can provide the means to detect errors that may occur in the physical layer, switches operate in this layer, data in this layer is organized into frames.
* **Layer 1: Phyiscal**: The phyiscal layer defines the details of how data is physcial