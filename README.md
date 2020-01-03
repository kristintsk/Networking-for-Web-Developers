# Networking for Web Developers / Udacity
## Kristin Tuisk

man nc (netcat manual)


### 1. Ülevaade kursuses kasutatud käsurea programmide ja näidete kohta.
**Use `ping -c3 8.8.8.8`**\
 -c means 'send 3 test-messages, then quit\
 8.8.8.8 is an address of a particular service at Google
 > ##### result received 
> 3 packets transmitted, 3 packets received, 0.0% packet loss
> meaning
> - my computer has Internet access
> - The computer at 8.8.8.8 is up and running
> - my ISP knows how to send and receive traffic towards and from Google
 
 **Use `printf 'HEAD / HTTP/1.1\r\nHost: www.google.com\r\n\r\n' | nc www.google.com 80`**  
printf is a command for printing formatted strings.
the netcat utility is used to create client-to-server connections (it can fulfill both server and client role).
pipe in the middle means that take the output from first request and use it as an input for the second request.
> ##### result received
> HTTP-header sent back by the server of Wikipedia (status code, cookies and other header fields)\
> e.g this is the way to find out what serves Google uses:\
> Server: gws\
> which means google web server

To save the results of an nc command to a file, use the > shell redirection operator. 
**use `printf "GET / HTTP/1.1\r\nHost: www.example.com\r\n\r\n" | nc www.example.com 80 > example.txt`**  
this will save the results to the file example.txt


** Use `nc -l 3456`** to start listening on a port.\
open another terminal and use **`nc localhost 3456`**\
this way it is possible to send and receive messages in both windows

**Use `ip addr show`**
  **See:** it shows at least two  


### 2. Ülevaade põhilistest võrguseadmetest ja nende ülesannetest:
- **Router (ruuter)**\
Router is a device that connects two different IP networks. It acts as a gateway - hosts forward the traffic through the router.

- **Switch (kohtvõrgukommutaator)**\

- **Firewall (tulemüür)**\

- **WiFi access point (WiFi tugijaam)**\


### 3. Võrguprotokollid ja nende kasutus:
- **SSH**\
SSH means **Secure Shell** and is a cryptographic network protocol for operating network services securely over an unsecured network.
     - Typical applications include remote command-line, login, and remote command execution, but any network service can be secured with SSH.
     - The protocol specification distinguishes between two major versions, referred to as SSH-1 and SSH-2. The standard TCP port for SSH is 22. 
     - SSH is generally used to access Unix-like operating systems, but it can also be used on Microsoft Windows. Windows 10 uses OpenSSH as its default SSH client.
     - SSH was designed as a replacement for Telnet and for unsecured remote shell protocols such as the Berkeley rlogin, rsh, and rexec protocols.

- **telnet** 

- **IMAP, POP3, SMTP**

- **SNMP**

- **HTTP, HTTPS**\
HTTP means **Hyper Text Transfer Protocol** which means it defines how messages are formatted and transmitted in WWW which is about communication between web clients and servers. Communication between client computers and web servers is done by sending HTTP Requests and receiving HTTP Responses.\

     - **HTTPS**\
HTTPS means **Hyper Text Transfer Protocol Secure**. Basically, it is the secure version of HTTP. Communications between the browser and website are encrypted by Transport Layer Security (TLS), or its predecessor, Secure Sockets Layer (SSL).     

- **DNS**\
DNS means **Domain Name System**, it's a worldwide distributed directory of network information. The best known DNS record is A-record, which is used to find the address of a computer connected to the internet.\
     - Web browsers interact through IP addresses. DNS translates domain names to IP addresses so browsers can load Internet resources.\ 
     - Each device connected to the Internet has a unique IP address which other machines use to find the device. DNS servers eliminate the need for humans to memorize IP addresses such as 192.168.1.1 (in IPv4), or more complex newer alphanumeric IP addresses such as 2400:cb00:2048:1::c629:d7a2 (in IPv6).\
     - A website creator needs to set up DNS records for users could access it by name. It usually involves registering the domain with a registrar and pointing the DNS records at the web servers IP adresses so that users could reach them.

- **NTP**

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
|     2^32    |   2^128    |

- **TCP**\
TCP means **Transmission Control Protocol** and is one of the main protocols of the Internet protocol suite. It originated in the initial network implementation in which it complemented the Internet Protocol (IP).\
TCP is kind of a middle layerof a stack of networking protocols or protocol stack that supports internet applications.
HTTP and other applications are built on top of TCP and TCP is built on top of IP


- **UDP**


- **ICMP**

### 4. Diagnostika vahendid:
- Wireshark
- tcpdump 

> - ping\
> Ping is a way to test wheather the computer is able to send and receive web requests.\
> Ping is simpler than HTTP, but HTTP is not based on ping.\

- traceroute / tracert
- nslookup / dig
- Ressource monitor (Windows)
- netstat 



 




http layer is implemented by programs, such as web browsers and servers, the lower level (TCP) is implemented in the operating system. The NC command is a thin wrapper over TCP.




Port numbers
On most systems the lowest 1024 ports (0 - 1023) are reserved for the programs that are started by the system superuser account or root at the Unix.
If you try to make nc listen on the same port number that another program is listening on, nc gives the error message 'the port is in use'.







#### Netblocks and subnet
  Intro
  > /22 network = 10 bits of host ports 
  >             = 2^10 addresses (3 reserved for ...)
  >             = 1021 adresses to use
  
  > /24 network = 8 bits of host ports
  >             = 2^8 addresses (3 reserved for ...)
  >             = 253 adresses to use
  
    

  
#### Routers and default gateways







