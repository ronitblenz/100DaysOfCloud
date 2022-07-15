![placeholder image](http://hu.edu.so/wp-content/uploads/2018/09/it.jpeg)

# Computer Networking

## Introduction

Computer networking refers to connected computing devices (such as laptops, desktops, servers, smartphones, and tablets) and an ever-expanding array of IoT devices (such as cameras, door locks, doorbells, refrigerators, audio/visual systems, thermostats, and various sensors) that communicate with one another.

This write-up will cover Computer Networking step-by-step.

## Protocols

 - **TCP (Transmission Control Protocol):** 
  It will ensure that the data will reach it's destination and it will not be corrupted in the way.
 - **UDP (User Datagram Protocol):** 
  All data may not reach the recepient. For example, Video Conferencing.
 - **HTTP (Hyper Text Transfer Protocol):** 
  Used to make web server <---> client requests.

## IP Address

![image](https://user-images.githubusercontent.com/91361382/179264638-25563ce6-a25d-4de4-804b-710abbe3efb6.png)

An Internet Protocol address (IP address) is a numerical label such as 192.0.2.1 that is connected to a computer network that uses the Internet Protocol for communication. An IP address serves two main functions: network interface identification and location addressing.

Internet Protocol version 4 (IPv4) defines an IP address as a 32-bit number. However, because of the growth of the Internet and the depletion of available IPv4 addresses, a new version of IP (IPv6), using 128 bits for the IP address, was standardized in 1998. IPv6 deployment has been ongoing since the mid-2000s.

 - 1 bit = 1 or 0
 - 00000000 = 0
 - 11111111 = 255
 - That's why IP address ranges from ```0.0.0.0``` --> ```255.255.255.255``` (In case of IPv4)
 - IPv6 are 128-bit number which consists of Hexadecimal values (16-bit each) like ```a.a.a.a.a.a.a.a```

## Switch and Router

![image](https://user-images.githubusercontent.com/91361382/179267171-7c94dae0-375d-4d31-8b63-ac17fcb9f52a.png)

 - Switches are networking devices that connect devices in a network and use packet switching to send, receive or forward data packets or data frames over the network.
 - Routers are networking devices that are responsible for receiving, analysing, and forwarding data packets among the connected computer networks.
 - **Key Difference between Switch and Router is:**
   Router mainly focuses to connect various networks where as Switch connects various devices.

## Subnet

![image](https://user-images.githubusercontent.com/91361382/179271208-e8aa4939-9aed-4dfd-bee8-1f09156b8f6b.png)

 - Subnet is the logical subdivision of an IP network
 - Subnetting is the process of dividing a network into two or more networks
 - Subnet Mask separates the IP address into the network and host addresses.


![image](https://user-images.githubusercontent.com/91361382/179271997-d317499f-fb1e-4bf3-956a-def6603e33ff.png)

 - It signifies that IP addresses starting with ```192.168.0.x``` belongs to the same LAN
 - Value 255 fixates the Octate (That octate cannot be modified to be assigned)
 - Value 0 means free range (That octate can be modified and assigned)

 - **To express this in simplified way, we use CIDR Block**

![image](https://user-images.githubusercontent.com/91361382/179279085-79b5f48d-7512-4f34-9bdc-fb1d87fc14b1.png)

## A Sample Network System

![image](https://user-images.githubusercontent.com/91361382/179279430-e71dedfa-bb76-46f1-8704-8be2c3fef01c.png)

## NAT 

![image](https://user-images.githubusercontent.com/91361382/179281031-92d285ef-917d-49a0-88b3-c54a93f275a5.png)

 - NAT stands for ```Network Address Translation```
 - This helps to replace the local device's IP address by the router
 - It is mainly there to Re-use IP Addresses and provide Security to the LAN
 - FUN FACT : We are limited to ```4,294,967,296``` IP Address (IPv4) available world wide

## Firewall

![image](https://user-images.githubusercontent.com/91361382/179281611-0e0ecfce-55f4-41f3-90f1-8e125bac30c6.png)

 - A firewall is a network security device that monitors incoming and outgoing network traffic and decides whether to allow or block specific traffic based on a defined set of security rules.

Firewalls have been a first line of defense in network security for over 25 years. They establish a barrier between secured and controlled internal networks that can be trusted and untrusted outside networks, such as the Internet.

## Port

![image](https://user-images.githubusercontent.com/91361382/179281694-6d75a2b7-2260-45d7-8217-5f47d02ba1ce.png)

 - A port is a virtual point where network connections start and end. Ports are software-based and managed by a computer's operating system. Each port is associated with a specific process or service. Ports allow computers to easily differentiate between different kinds of traffic: emails go to a different port than webpages, for instance, even though both reach a computer over the same Internet connection.

## DNS

![image](https://user-images.githubusercontent.com/91361382/179281920-ea27ce8b-f59b-41dc-8161-720491bd9cd5.png)

 - DNS is a hostname for IP address translation service. DNS is a distributed database implemented in a hierarchy of name servers. It is an application layer protocol for message exchange between clients and servers. 
 - **Popular Generic Domains are as follows :**

![image](https://user-images.githubusercontent.com/91361382/179282124-14dac8e8-631d-4bd0-9a49-c0dc10507bd7.png)

 - **The Root DNS Servers are as follows :**

![image](https://user-images.githubusercontent.com/91361382/179282340-9c064b61-6a24-4e3a-9ee5-9ea05cee4258.png)

 - The Domains and Root DNS Servers are maintained by ```ICANN``` (Internet Corporation for Assigned Names and Numbers)

## Basic Network Commands


 - ```ifconfig``` --> configure the kernel-resident network interfaces
 - ```netstat``` --> monitoring network connections both incoming and outgoing as well as viewing routing tables, interface statistics, etc
 - ```ps aux``` --> print all processes owned by a user named "x", as well as printing all processes that would be selected by the -a option
 - ```nslookup``` --> query Internet domain name servers for information
 - ```ping``` --> check the network connectivity between host and server/host
 
 ## OSI Model

- The OSI Model (Open Systems Interconnection Model) is a conceptual framework used to describe the functions of a networking system. The OSI model characterizes computing functions into a universal set of rules and requirements in order to support interoperability between different products and software.

- **It is broadly classified into 5 Layers :**
 1. Application Layer
 2. Transport Layer
 3. Network Layer
 4. Data Link Layer
 5. Physical Layer

- The **Application Layer** is the layer that users interact with and use. The application layer allows users to send data, access data and use networks. The layers also facilitate communication and sometimes allows user to use software programs.
- The **Transport Layer** provides services to the application layer and takes services from the network layer. The data in the transport layer is referred to as Segments. It is responsible for the End to End Delivery of the complete message. The transport layer also provides the acknowledgement of the successful data transmission and re-transmits the data if an error is found.
- The **Network Layer** works for the transmission of data from one host to the other located in different networks. It also takes care of packet routing i.e. selection of the shortest path to transmit the packet, from the number of routes available. The sender & receiver’s IP addresses are placed in the header by the network layer. 
- The **Data Link Layer** is responsible for the node-to-node delivery of the message. The main function of this layer is to make sure data transfer is error-free from one node to another, over the physical layer. When a packet arrives in a network, it is the responsibility of DLL to transmit it to the Host using its MAC address. 

Data Link Layer is divided into two sublayers:  

  i. Logical Link Control (LLC)
  ii. Media Access Control (MAC)
 
- The **Physical Layer** is responsible for the actual physical connection between the devices. The physical layer contains information in the form of bits. It is responsible for transmitting individual bits from one node to the next. When receiving data, this layer will get the signal received and convert it into 0s and 1s and send them to the Data Link layer, which will put the frame back together.  

_"This is how basically Internet works !"_

Thanks for reading till the very end.

Follow me on [Twitter](https://twitter.com/ronitblenz), [LinkedIn](https://www.linkedin.com/in/ronitbanerjee/) and [GitHub](https://github.com/ronitblenz) for more amazing blogs about Cloud, DevOps and More !
