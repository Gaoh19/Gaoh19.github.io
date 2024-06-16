---
title: Pre Security
time: 2024-06-16 12:00:00
categories: [Infosec, Research]
tags: [preSecurity, infoSec]
image: /assets/posts/PreSecurity/p1.png
---

Well, I decided to take up this path to brush up on the basics, I see some of the modules have some good content. Without further ado, let’s get to it. Woah that was the first time I typed the word `ado` , had to google it to confirm the spelling LOL.

## Networking

The first iteration of the Internet was within the `ARPANET` project in the late 1960s. This project was funded by the United States Defense Department and was the first documented network in action. However, it wasn't until 1989 when the Internet as we know it was invented by Tim Berners-Lee by the creation of the **W**orld **W**ide **W**eb (**`WWW`**). It wasn't until this point that the Internet started to be used as a repository for storing and sharing information, just like it is today.

The IP (Internet Protocol) address is made up of 4 octets. These values are calculated through a technique known as `IP Subnetting.` 

IPv6 is a new iteration of the Internet Protocol addressing scheme to help tackle this issue. Although it is seemingly more daunting, it boasts a few benefits:

- Supports up to 2^128 of IP addresses (340 trillion-plus), resolving the issues faced with IPv4
- More efficient due to new methodologies

Devices on a network will all have a physical network interface, which is a microchip board found on the device's motherboard. This network interface is assigned a unique address at the factory it was built at, called a **`MAC` (**M**edia A**ccess **C**ontrol ) address. The MAC address is a **twelve-character** hexadecimal number (*a base sixteen numbering system used in computing to represent numbers*) split into two's and separated by a colon. These colons are considered separators. For example, `a4:c3:f0:85:ac:2d`. The first six characters represent the company that made the network interface, and the last six is a unique number.

If you look closely, the markdown is a mess in the above paragraph.
Now, I’ll be going on a wild detour, learning about the things discussed above in detail. Of course, the OG `ChatGPT` will be one with all the data.

IP Subnetting is a technique used to divide a larger network into smaller, more manageable sub-networks or subnets. This helps in efficient IP address management, improves network performance, and enhances security.

![p1](/assets/posts/PreSecurity/p1.png)

A subnet mask is used to divide the IP address into the network and host portions. It determines which part of the IP address identifies the network and which part identifies the host. The subnet mask also consists of four octets and is written in the same format as an IP address. For example, `255.255.255.0`.

`Octets and Binary Representation`

- Each octet in an IP address or subnet mask is an 8-bit binary number.
- For example, the IP address `192.168.1.1` in binary is `11000000.10101000.00000001.00000001`.
- Similarly, the subnet mask `255.255.255.0` in binary is `11111111.11111111.11111111.00000000`.

`Subnetting Process`

1. **Determine the Network and Host Portions:**
    - The subnet mask is used to determine the network and host portions of an IP address.
    - For instance, with a subnet mask of `255.255.255.0`, the first three octets (`255.255.255`) represent the network portion, and the last octet (`0`) represents the host portion.
2. **Subnetting the Network:**
    - To create subnets, we borrow bits from the host portion of the address to create additional network bits.
    - For example, if we borrow one bit from the host portion in a Class C network (default subnet mask `255.255.255.0`), the new subnet mask becomes `255.255.255.128` (`11111111.11111111.11111111.10000000` in binary).
3. **Calculate the Number of Subnets and Hosts:**
    - The number of subnets is calculated as `2^n` where `n` is the number of bits borrowed.
    - The number of hosts per subnet is calculated as `2^h - 2` where `h` is the number of remaining host bits (subtracting 2 accounts for the network and broadcast addresses).
    - For example, borrowing one bit in a Class C network creates `2^1 = 2` subnets, and each subnet can have `2^7 - 2 = 126` hosts.

`Example`

Given an IP address `192.168.1.0` and a subnet mask `255.255.255.0`, let's subnet it:

1. Borrow 2 bits from the host portion:
    - New subnet mask: `255.255.255.192` (`11111111.11111111.11111111.11000000`).
2. Calculate the number of subnets:
    - `2^2 = 4` subnets.
3. Calculate the number of hosts per subnet:
    - `2^6 - 2 = 62` hosts per subnet.
4. Subnets created:
    - Subnet 1: `192.168.1.0` to `192.168.1.63`
    - Subnet 2: `192.168.1.64` to `192.168.1.127`
    - Subnet 3: `192.168.1.128` to `192.168.1.191`
    - Subnet 4: `192.168.1.192` to `192.168.1.255`

Each subnet has its own range of IP addresses, with the first address reserved as the network address and the last address reserved as the broadcast address. This subnetting process allows better organization and management of IP addresses within a network.

That explanation was beautiful. Now we’ll look at the types of network Protocols. Juicy content ahead. Be prepared !

### Network Protocols

IP addresses operate within a framework of standards and protocols that ensure reliable and consistent communication across networks. These protocols are part of the larger TCP/IP suite, which is fundamental to internet and network communication. Here are some key protocols related to IP addresses:

`1. Internet Protocol (IP)`

- **IPv4 (Internet Protocol Version 4):**
    - Uses a 32-bit address space, providing about 4.3 billion unique addresses.
    - Written in decimal format (e.g., 192.168.1.1).
    - Includes features such as addressing, fragmentation, and routing.
- **IPv6 (Internet Protocol Version 6):**
    - Uses a 128-bit address space, providing a virtually limitless number of unique addresses.
    - Written in hexadecimal format (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334).
    - Designed to address IPv4 exhaustion and includes improvements such as simplified header format and enhanced security.

`2. Transmission Control Protocol (TCP)`

Ensures reliable, ordered, and error-checked delivery of data between applications.

Establishes a connection before data transfer and ensures that data packets are delivered in the correct order.

`3. User Datagram Protocol (UDP)`

Provides a connectionless communication method.

Focuses on low-latency and reduced overhead, suitable for applications where speed is critical, such as streaming and gaming.

Does not guarantee delivery, order, or error checking.

`4. Address Resolution Protocol (ARP)`

Its job is to find the hardware address of a host from a known IP address. ARP has several types: Reverse ARP, Proxy ARP, Gratuitous ARP, and Inverse ARP.

Translates IP addresses to MAC (Media Access Control) addresses within a local network.

Essential for network communication where devices need to identify each other by their physical hardware addresses.

`5. Reverse Address Resolution Protocol (RARP)`

Used by a device to determine its IP address using its MAC address. Useful for diskless workstations that need to discover their IP address upon booting.

`6. Dynamic Host Configuration Protocol (DHCP)`

DHCP – Dynamic Host Configuration Protocol is a network management protocol that we use on TCP/IP Network. The DHCP server, automatically assigns IP addresses and other network configurations like `Subnet Mask, Default Gateway, DNS Server`, and more to the connected devices so they can exchange information. DHCP let the hosts get the necessary TCP/IP configuration data from the DHCP server. Automatic IP Assignment.

A device makes a request for an IP address if it wants to gain access to a network that’s utilizing DHCP. The server replies and provides an IP address to the device. After that, it monitors the use of the address, and when a defined period expires, or the device shuts down, it takes it back to its pool of available IP addresses. It is kept until it has to be reassigned to a different device that wants to access the network.

Using this protocol, the network administrators, don’t need to set a static IP for each device, and later reassign it to another and keep an eye on all the available IPs. They will just set up the DHCP server with all the additional network information, and it will do its work dynamically.

![p2](/assets/posts/PreSecurity/p2.png)

The server gets the accepting message from the device. It will provide the IP address to the device, together with the subnet mask and the DNS server. It will write a record with the information of the newly connected device that usually includes the MAC address of the connected device, the IP address that was assigned, and the expiration date of that IP address. The DHCP leases the IP address for a limited time only. After the time passes, the IP address will go back to the IP pool of available IP addresses and can be assigned to a new device again.

`7. Internet Control Message Protocol (ICMP)`

Used for diagnostic and error-reporting purposes.

Utilized by tools like `ping` and `traceroute` to test connectivity and network performance.

`8. Network Address Translation (NAT)`

Allows multiple devices on a local network to share a single public IP address.

Modifies network address information in packet headers while in transit, enabling communication between devices in different networks.

`9. Simple Network Management Protocol (SNMP)`

Used for network management and monitoring. Allows administrators to collect and organize information about managed devices on IP networks.

`10. Domain Name System (DNS)`

Translates human-readable domain names (e.g., `www.example.com`) into IP addresses.

Ensures users can access websites using easy-to-remember names rather than numerical IP addresses.

`11. Border Gateway Protocol (BGP)`

Manages how packets are routed across the internet through the exchange of routing information between ISPs. Ensures data takes the best path through the complex web of networks.

`12. Open Shortest Path First (OSPF)`

An interior gateway protocol used for routing within a single autonomous system.

Utilizes the shortest path first (SPF) algorithm to determine the most efficient route for data.

These protocols collectively ensure the smooth operation of IP networks, enabling devices to communicate efficiently, securely, and reliably across local and global networks.

Now, let’s go into Public and Private IPs in detail.

### Public vs. Private IP Addresses

IP addresses are classified into two main types: public and private. These classifications determine how devices interact within networks and how they connect to the broader internet. Understanding the distinction between public and private IP addresses is crucial for network management, security, and efficient use of address space.

**`Public IP Addresses`**

**Concept:**

- Public IP addresses are globally unique and assigned by Internet Service Providers (ISPs).
- They are used to identify devices that are directly accessible over the internet.

**Key Points:**

1. **Uniqueness:**
    - Each public IP address must be unique across the entire internet to prevent address conflicts.
    - Managed by organizations like IANA (Internet Assigned Numbers Authority) and regional registries (e.g., ARIN, RIPE NCC).
2. **Accessibility:**
    - Devices with public IP addresses can be accessed from anywhere on the internet.
    - Examples include web servers, email servers, and routers.
3. **Allocation:**
    - Assigned to devices by ISPs.
    - Typically, home users get one public IP address, while businesses may get multiple.
4. **Address Range:**
    - Public IP addresses range from 1.0.0.0 to 223.255.255.255, excluding the reserved and private address spaces.

**Example:**

- A home router with a public IP address like `203.0.113.1` connects to the internet, allowing users to access websites and services worldwide.

**`Private IP Addresses`**

**Concept:**

- Private IP addresses are used within private networks (e.g., home, office, enterprise networks) and are not routable on the internet.
- They provide internal network communication and conserve the global IP address space.

**Key Points:**

1. **Range:**
    - Defined by the IETF in RFC 1918.
    - There are three private IP address ranges:
        - **Class A:** `10.0.0.0` to `10.255.255.255`
        - **Class B:** `172.16.0.0` to `172.31.255.255`
        - **Class C:** `192.168.0.0` to `192.168.255.255`
2. **Non-Unique:**
    - Private IP addresses do not need to be globally unique.
    - They can be reused in different private networks without conflict.
3. **Usage:**
    - Used for internal communication within a local network.
    - Examples include devices like computers, smartphones, printers, and IoT devices in a home or office network.
4. **Address Translation:**
    - To communicate with the internet, devices with private IP addresses require Network Address Translation (NAT) provided by a router or gateway.
    - NAT translates private IP addresses to a public IP address for internet access.

**Example:**

- Devices in a home network might have private IP addresses like `192.168.1.2`, `192.168.1.3`, etc. The home router then translates these addresses to a single public IP address for internet communication.

**`Network Address Translation (NAT)`**

**Concept:**

- NAT is a technique used to map private IP addresses to a public IP address for communication with external networks.

**Key Points:**

1. **Functionality:**
    - NAT allows multiple devices on a local network to share a single public IP address.
    - Translates internal private IP addresses to the public IP address of the router for outgoing traffic.
    - Maintains a translation table to route incoming traffic to the correct private IP address.
2. **Types:**
    - **Static NAT:** Maps a single private IP address to a single public IP address.
    - **Dynamic NAT:** Maps a private IP address to a public IP address from a pool of public addresses.
    - **PAT (Port Address Translation):** Also known as "NAT overload," maps multiple private IP addresses to a single public IP address using different ports.
3. **Advantages:**
    - Conserves the global IP address space.
    - Adds a layer of security by hiding internal network structure from the outside world.

**Example:**

- A home network with multiple devices (e.g., `192.168.1.2`, `192.168.1.3`) uses NAT to share a single public IP address (e.g., `203.0.113.1`) provided by the ISP. The router handles the translation of internal addresses to the public address for internet access.

`Summary`

- **Public IP addresses** are globally unique, assigned by ISPs, and necessary for devices directly accessible over the internet.
- **Private IP addresses** are used within local networks, not routable on the internet, and allow for internal communication without consuming global address space.
- **NAT** enables devices with private IP addresses to communicate with the internet by translating private addresses to a public address, conserving IP addresses, and providing an additional security layer.

Well, that was a clean explanation, well point to note is about NAT, you would really care about it when you configure your VMs ( Virtual Machines ) to have a specific class of IP, or making it connect to the internet with NAT or Bridged Adapter features and so on. We’ll explore that later.

Next, We’ll learn about ISPs and how they provide IP services,

### ISP Services

When you subscribe to an internet service from an Internet Service Provider (ISP), they assign you a public IP address that is used for all your devices within your local network to communicate with the broader internet. Here’s a detailed explanation of how this process works:

`Dynamic IP Assignment by ISP`

1. **Dynamic IP Allocation:**
    - ISPs typically use Dynamic Host Configuration Protocol (DHCP) to assign public IP addresses dynamically.
    - When you connect your modem or router to the ISP’s network, it sends a request to the ISP’s DHCP server.
    - The DHCP server assigns a public IP address to your modem/router from a pool of available IP addresses.
    - This IP address can change periodically or remain the same for extended periods, depending on the ISP’s policies.

`Role of the Router and NAT`

1. **Router Functionality:**
    - Your modem connects to the ISP’s network and receives the public IP address.
    - The modem is often connected to a router, which manages your local network (LAN).
2. **Network Address Translation (NAT):**
    - The router uses a technology called Network Address Translation (NAT) to enable multiple devices on your local network to share the single public IP address assigned by the ISP.
    - Each device within your local network is assigned a unique private IP address (e.g., 192.168.1.2, 192.168.1.3) by the router using its own DHCP server.
3. **How NAT Works:**
    - When a device in your local network sends data to the internet, the router translates the private IP address of the device to the public IP address assigned by the ISP.
    - The router also keeps track of the original private IP address and port number in a NAT table, so it knows how to route the return traffic back to the correct device.
    - For example, if device A (192.168.1.2) sends a request to a web server, the router replaces the private IP address with the public IP address and forwards the request. When the web server responds, the router uses the NAT table to map the incoming response back to device A.

`Example of NAT in Action`

- **Internal Network Communication:**
    - Device A (192.168.1.2) and Device B (192.168.1.3) communicate directly using their private IP addresses without involving NAT or the public IP address.
- **External Communication:**
    - Device A wants to access a website on the internet.
    - Device A sends a request to the router.
    - The router translates Device A’s private IP (192.168.1.2) to the public IP (e.g., 203.0.113.1) and sends the request to the website.
    - The website sends a response to the public IP address (203.0.113.1).
    - The router receives the response, checks the NAT table, and forwards the response to Device A (192.168.1.2).

`Benefits of This Approach`

1. **IP Address Conservation:**
    - By using NAT, multiple devices on your local network can share a single public IP address, which helps conserve the limited number of available IPv4 addresses.
2. **Security:**
    - NAT provides an additional layer of security because external devices on the internet can only see the public IP address and not the individual private IP addresses of devices within your local network.
    - This makes it harder for potential attackers to directly target individual devices within your network.

`ISP's Role and Billing`

- **ISP Assignment:**
    - ISPs manage large pools of public IP addresses and assign them to customers as needed.
    - The IP address allocation can be static (fixed) or dynamic (changing periodically).
- **Billing:**
    - ISPs charge customers for internet service, which typically includes the assignment of a public IP address.
    - The cost may vary based on the type of service, speed, and additional features like a static IP address or enhanced security.

In summary, your ISP assigns a public IP address to your modem/router, and your router uses NAT to enable multiple devices in your local network to share this public IP address for internet access. This setup allows efficient use of IP addresses and adds a layer of security for your local network.

Well, that is that for the brief detour on IPs, NATs and DHCPs. We’ll be continuing on THM.

![Continue](/assets/posts/PrivEscalation/continue.jpg)