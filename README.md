# Networking for Web Developers / Udacity
## Kristin Tuisk

man nc (netcat manual)

### 1. Ülevaade kursuses kasutatud käsurea programmide ja näidete kohta
**Used `ping -c3 8.8.8.8`**\
- -c means 'send 3 test-messages, then quit\
- 8.8.8.8 is an address of a particular service at Google  
      - received expected result: 3 packets transmitted, 3 packets received, 0.0% packet loss meaning  
           - my computer has Internet access  
           - the computer at 8.8.8.8 is up and running  
           - my ISP knows how to send and receive traffic towards and from Google    
 
 **Used `printf 'HEAD / HTTP/1.1\r\nHost: www.google.com\r\n\r\n' | nc www.google.com 80`**  
printf is a command for printing formatted strings.
the netcat utility is used to create client-to-server connections (it can fulfill both server and client role).
pipe in the middle means that take the output from first request and use it as an input for the second request.
     - suceeded to receive the expected data
> HTTP-header sent back by the server of Wikipedia (status code, cookies and other header fields)\
> e.g this is the way to find out what serves Google uses:\
> Server: gws\
> which means google web server

To save the results of an nc command to a file, use the > shell redirection operator.\
**used `printf "GET / HTTP/1.1\r\nHost: www.example.com\r\n\r\n" | nc www.example.com 80 > example.txt`**  
did not manage to find the file.


** Used `nc -l 3456`** to start listening on a port.\
opened another terminal and used **`nc localhost 3456`**\
this way made it possible to send and receive messages in both windows

**Used `ip addr show`**
  **See:** it shows at least two  
 
**Used `sudo tcpdump -n host 8.8.8.8`** in first and run `ping -c3 8.8.8.8` in second Terminal
for each ping tcpdump shows two packages' records - request and reply.
end with Ctrl + C

tcpdump -n port 53 (4-3 at 2:32)
tcpdump -n port 80 (4-4)

host command in dns?

**Used `traceroute google.com`**
was ecpecting to see a lot of data including IP addresses and milliseconds
actual result was: information, that max 30 hops, the first line showed some information, the naxt 29 lines all showed * * * 
     - found out that traceoute requires a response from the target server and each of the intermediate hops to create its output. If a router doesn't generate a `Time-to-live exceeded` response, traceroute will not know anything about that hop. a hop that outputs `* * *` means that the router at that hop doesn't respond to the type of packet I was using for the traceroute (by default it's UDP on Unix-like and ICMP on Windows).
     - also a following suggestion: "If you are using the same version of traceroute I have you can try using the -e option to try to evade firewalls and the -P option to use ICMP, TCP or GRE packets instead of UDP. You can also try specifying a particular port that is unlikely to be filtered (such as 80 or 25) using the -p option."
     - **how to use those things?**
     

### 2. Ülevaade põhilistest võrguseadmetest ja nende ülesannetest

- **Router (ruuter)**\
Router is a device that connects two different IP networks. It acts as a gateway - hosts forward the traffic through the router.
     - A router is connected to two or more data lines from different IP networks.
     - When a data packet comes in on one of the lines, the router reads the network address information in the packet header to determine the ultimate destination. 
     - Then, using information in its routing table or routing policy, router directs the packet to the next network on its journey.

- **Switch (kohtvõrgukommutaator)**\
**A network switch** (also called switching hub, bridging hub, officially MAC bridge) is networking hardware that connects other devices together. 
     - Multiple data cables are plugged into a switch to enable communication between different networked devices. 
     - Switches manage the flow of data across a network by transmitting a received network packet only to the one or more devices for which the packet is intended. 
     - Each networked device connected to a switch can be identified by its network address, allowing the switch to direct the flow of traffic maximizing the security and efficiency of the network.

- **Firewall (tulemüür)**\
Firewalls are devices that network operators can use to filter traffic that's coming into or leaving their network. 
     - The most common configuration for a firewall is to drop any incoming traffic except traffic to (host, port) pairs that are supposed to be receiving connections from the Internet. This lets the network administrator be sure that other machines on the network — like backend databases or administrative systems — aren’t going to get direct attacks from outside.
     - Firewalls can cause trouble for application developers when testing the app - they can potentially interfere with the app or block it completely. One of the reasons that many non-Web applications use HTTP as a transport is that HTTP is often unblocked at firewalls even when other ports are blocked.
     - Aside from blocking traffic outright, middleboxes (e.g. firewall) can also alter traffic, for instance replacing web pages with error messages. This is often done for social or political purposes.

- **WiFi access point (WiFi tugijaam)**\
**A wireless access point (WAP), or more generally just access point (AP)**, is a networking hardware device that allows other Wi-Fi devices to connect to a wired network. 
     - The AP usually connects to a router (via a wired network) as a standalone device, but it can also be an integral component of the router itself. 
     - An AP is differentiated from a hotspot, which is the physical location where Wi-Fi access to a WLAN is available.
     - **WLAN (a wireless LAN)** is a wireless computer network that links two or more devices using wireless communication to form a local area network (LAN) within a limited area such as a home, school etc.


### 3. Võrguprotokollid ja nende kasutus

- **SSH**\
SSH means **Secure Shell** and is a cryptographic network protocol for operating network services securely over an unsecured network.
     - Typical applications include remote command-line, login, and remote command execution, but any network service can be secured with SSH.
     - The protocol specification distinguishes between two major versions, referred to as SSH-1 and SSH-2.
     - SSH is generally used to access Unix-like operating systems, but it can also be used on Microsoft Windows. Windows 10 uses OpenSSH as its default SSH client.
     - SSH was designed as a replacement for Telnet and for unsecured remote shell protocols such as the Berkeley rlogin, rsh, and rexec protocols.

- **telnet**\
The name stands for "teletype network". Telnet is a client-server protocol used on the Internet or local area network to provide a bidirectional interactive text-oriented communication facility using a virtual terminal connection. User data is interspersed in-band with Telnet control information in an 8-bit byte oriented data connection over the Transmission Control Protocol (TCP).
     - Typically, this protocol is used to establish a connection to Transmission Control Protocol (TCP) port number 23.
     - To telnet means to establish a connection using the Telnet protocol, either with a command line client or with a graphical interface.
     - Telnet provided access to a command-line interface on a remote host. Because of serious security concerns when using Telnet over an open network such as the Internet, its use for this purpose has waned significantly in favor of SSH.

- **IMAP, POP3, SMTP**
     - **Internet Message Access Protocol (IMAP)** and is an Internet standard protocol used by email clients to retrieve email messages from a mail server over a TCP/IP connection.
     - IMAP was designed with the goal of permitting complete management of an email box by multiple email clients.
     - Virtually all modern e-mail clients and servers support IMAP, which along with the earlier **POP3 (Post Office Protocol)** are the two most prevalent standard protocols for email retrieval.
     - Many webmail service providers such as Gmail, Outlook.com and Yahoo! Mail also provide support for both IMAP and POP3.
     - **Simple Mail Transfer Protocol (SMTP)** is a communication protocol for electronic mail transmission. Mail servers and other message transfer agents use SMTP to send and receive mail messages. 
     - Proprietary systems such as Microsoft Exchange and IBM Notes and webmail systems such as Outlook.com, Gmail and Yahoo! Mail may use non-standard protocols internally, but all use SMTP when sending to or receiving email from outside their own systems.
     - User-level email clients typically use SMTP only for sending messages to a mail server for relaying. For retrieving messages, IMAP and POP3 are standard, but proprietary servers also often implement proprietary protocols, e.g., Exchange ActiveSync.

- **SNMP**\
SNMP means **Simple Network Management Protocol** and is an Internet Standard protocol for collecting and organizing information about managed devices on IP networks and for modifying that information to change device behavior. Devices that typically support SNMP include cable modems, routers, switches, servers, workstations, printers, and more.

- **HTTP**\
HTTP means **Hyper Text Transfer Protocol** which means it defines how messages are formatted and transmitted in WWW which is about communication between web clients and servers. Communication between client computers and web servers is done by sending HTTP Requests and receiving HTTP Responses.\
     - The first documented version of HTTP was HTTP V0.9 (1991).

- **HTTPS**\
HTTPS means **Hyper Text Transfer Protocol Secure**. Basically, it is the secure version of HTTP. Communications between the browser and website are encrypted by Transport Layer Security (TLS), or its predecessor, Secure Sockets Layer (SSL).    
     - The authentication aspect of HTTPS requires a trusted third party to sign server side digital certificates, which historically was expensive. 
     - In 2016 a non profit organisation, Let's Encrypt, began to offer free server certificates to all, and a campaign by the Electronic Frontier Foundation and support of web browser developers led to the protocol to become more prevalent.
     - HTTPS is now used more often by web users than the original non-secure HTTP, primarily to protect page authenticity on all types of websites; secure accounts; and to keep user communications, identity, and web browsing private.

- **DNS**\
DNS means **Domain Name System**, it's a worldwide distributed directory of network information. The best known DNS record is A-record, which is used to find the address of a computer connected to the internet.\
     - Web browsers interact through IP addresses. DNS translates domain names to IP addresses so browsers can load Internet resources.\ 
     - Each device connected to the Internet has a unique IP address which other machines use to find the device. DNS servers eliminate the need for humans to memorize IP addresses such as 192.168.1.1 (in IPv4), or more complex newer alphanumeric IP addresses such as 2400:cb00:2048:1::c629:d7a2 (in IPv6).\
     - A website creator needs to set up DNS records for users could access it by name. It usually involves registering the domain with a registrar and pointing the DNS records at the web servers IP adresses so that users could reach them.

- **NTP**\
NTP means **Network Time Protocol** and is a networking protocol for clock synchronization between computer systems over packet-switched, variable-latency data networks. In operation since before 1985, NTP is one of the oldest Internet protocols in current use.
     - NTP is intended to synchronize all participating computers to within a few milliseconds of Coordinated Universal Time (UTC).

- **IP address**\
**IP means Internet Protocol** and IP address is the device's "digital address" - a numerical label assigned to each device connected to a computer network that uses the Internet > Protocol for communication. An IP address serves two main functions: host or network interface identification and location addressing.

     - IPv4\
The common type of IP address is known as IPv4, for "version 4", it defines an IP address as a 32-bit number and supports a maximum of approximately 4.3 billion unique IP addresses. IP addresses are written and displayed in human-readable notations, such as 172.16.254.1 in IPv4.

     - IP addresses don't belong to hosts, they belong to interfaces on hosts\
A host can have multiple network interfaces and each interface can have zero or more IP-addresses.

     - Reserved IP addresses\
There are more than a billion pubic addresses, but less than the population of the world. 
Over 1/8 of all possible IPv4 addressses are set aside for something other than addressing public hosts.

     - IPv6\
Because of the growth of the Internet and the depletion of available IPv4 addresses, a new version of IP (IPv6), using 128 bits for the IP address, was standardized in 1998. IPv6 supports, in theory, a maximum number that will never run out.

          |     IPv4      |      IPv6     |
          | ------------- | ------------- |
          |    32-bits    |   128-bits    |
          |    4 octets   |   16 octets   |
          |     2^32      |   2^128       |

- **TCP**\
TCP means **Transmission Control Protocol** and is one of the main protocols of the Internet protocol suite. It originated in the initial network implementation in which it complemented the Internet Protocol (IP).
     - one of the most important performance-feature for TCP is **TCP Congestion Control** - the endpoints and the routers in the middle collaborate to move data at close to an optimal speed.

- **UDP**\
UDP means **User Datagram Protocol** and is a simple message-oriented transport layer protocol being one of the core members of the Internet Protocol suite. UDP uses a simple connectionless communication model with a minimum of protocol mechanisms, there is no guarantee of delivery, ordering, or duplicate protection.
     - It is transaction-oriented, suitable for simple query-response protocols such as the DNS or the NTP.
     - It provides datagrams, suitable for modeling other protocols such as IP tunneling or remote procedure call and the NFS.
     - It is simple, suitable for bootstrapping or other purposes without a full protocol stack, such as the DHCP and Trivial File Transfer Protocol.
     - It is stateless, suitable for very large numbers of clients, such as in streaming media applications such as IPTV.
     - The lack of retransmission delays makes it suitable for real-time applications such as Voice over IP, online games, and many protocols using Real Time Streaming Protocol.
     - Because it supports multicast, it is suitable for broadcast information such as in many kinds of service discovery and shared information such as Precision Time Protocol and Routing Information Protocol.

- **ICMP**\
ICMP means **Internet Control Message Protocol** and is a supporting protocol in the Internet protocol suite. It is used by network devices, including routers, to send error messages and operational information indicating success or failure when communicating with another IP address, for example, an error is indicated when a requested service is not available or that a host or router could not be reached.
     - ICMP differs from transport protocols such as TCP and UDP in that it is not typically used to exchange data between systems, nor is it regularly employed by end-user network applications (with the exception of some diagnostic tools like ping and traceroute).
     - for IPv6 there is ICMPv6 which is an integral part of IPv6 and performs error reporting and diagnostic functions (e.g., ping), and has a framework for extensions to implement future changes.


### 4. Diagnostic utilities (diagnostika vahendid)

- **Wireshark**\

- **tcpdump**\
tcpdump is a common packet analyzer that runs under the command line. It allows the user to display TCP/IP and other packets being transmitted or received over a network to which the computer is attached. tcpdump can be used to monitor traffic for any network application.
     - The original TCP packet format has six flags. For each packet tspdump shows which flags are set on that packet.
     - ICMP (protocol used by ping) and UDP (used by basic DNS lookups) do not have TCP flags or sequence numbers.

- **ping**\
Ping is a way to test wheather the computer is able to send and receive web requests. Ping measures the round-trip time for messages sent from the originating host to a destination computer that are echoed back to the source.
     - Ping is simpler than HTTP, but HTTP is not based on ping.\

- **traceroute/tracert**\
Traceroute shows all the hops involved in getting a traffic from client to a distant server - it will display the route, all the IP addresses of all the routers that it took for traffic to get there.
     - more advanced traceroute tool is MTR - it will repeatedly trace and can sometimes show different routes that traffic may take.


- **nslookup/dig**\
The NsLookup tool allows you to query DNS servers for resource records. NsLookup queries the specified DNS server and retrieves the requested records that are associated with the domain name you provided. These records contain information like the domain name’s IP addresses.

- **Ressource monitor (Windows)**\


- **netstat**\
Netstat (network statistics) is a command-line network utility that displays network connections for 
     - Transmission Control Protocol (both incoming and outgoing), 
     - routing tables, 
     - and a number of network interface (network interface controller or software-defined network interface) and network protocol statistics.
Netstat is used for finding problems in the network and to determine the amount of traffic on the network as a performance measurement.
