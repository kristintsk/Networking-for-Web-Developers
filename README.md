# Networking for Web Developers / Udacity
## Kristin Tuisk

### Lesson 1 - From Ping to HTTP



### Lesson 2 - Names and Addresses




### Lesson 3 - Addressing and Networks
#### Reserved IP addresses
  There are more than a billion pubic addresses, but less than the population of the world. Over 1/8 of all possible IPv4 addressses are set aside for something other than addressing public hosts.

#### Netblocks and subnet
  Intro
  > /22 network = 10 bits of host ports 
  >             = 2^10 addresses (3 reserved for ...)
  >             = 1021 adresses to use
  
  > /24 network = 8 bits of host ports
  >             = 2^8 addresses (3 reserved for ...)
  >             = 253 adresses to use
  
    
#### IP addresses don't belong to hosts
  A host can have multiple network interfaces and each interface can have zero or more IP-addresses.
  **Use `ip addr show`**
  **See:** it shows at least two  
  
#### Routers and default gateways
Router is a device that connects two different IP networks. It acts as a gateway - hosts forward the traffic through the router.




#### IPv4 and IPv6
|     IPv4      |      IPv6     |
| ------------- | ------------- |
|    32-bits    |   128-bits    |
|    4 octets   |   16 octets   |
|     2^32    |   2^128    |

### Lesson 4 - Protocol Layers



### Lesson 5 - Big Networks
