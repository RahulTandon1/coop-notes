Source: https://www.youtube.com/watch?v=bj-Yfakjllc&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=1&ab_channel=PracticalNetworking

> How data moves through the internet

Networking devices - hosts, routers, hubs, repeaters, bridges, switches.


Host - anything that sends or receives traffic

Hosts are commonly categorised into Clients, which makes requests, and Servers which respond to requests.

Server just has special software for responding to certain types of requests.

> refl: host is not necessarily a computer that hosts a server.


**IP Address**
- 32-bit unique identifier for hosts.
- are hierarchically assigned (subnetting)
- when we send data in a network, the data has the src and destination ip addresses written on it.

Network - 
"logical grouping of hosts with similar connectivity requirements"
Solves the problem of needing to use a USB every time one wanted to transfer a file from computer A to B.


Repeaters - regenerate (not amplify) signals for long distance communication. Solves the problem of data on a wire decaying with increasing distance.

Hubs - repeaters but for multiple devices. "Multi-port repeaters."

Bridge 
- conditionally sends traffic across 2 networks (which are connected via hubs)
- Learns which nodes are on either side.


Switches
- Like a combination of Bridge and Hub.

-> hosts on a network share the same IP address space.

Routers
- communication between networks that it's in.
	- has an IP address on that network.
- traffic control points between networks.
- learn which networks its attached to, called routes. Stored in routing table.
- gateway: a hosts way oulet of its local network 
- routing table - encapsulates all the networks a router knows about.

#### OSI Model
- all hosts need to follow some rules for data to flow, or networking to work. Call these rules the OSI model and categorize them into 7 layers.
Layers:
- I think each layer has associated with it a header.
1. Physical Layer - transport bits layer
	includes wires, wifi, repeaters, hubs
2. Data Link layer - hop-to-hop
	addressing scheme - MAC address (48 bits)
	 this layers includes switches.
1. Network layer - end to end
	addressing scheme - IP address (32 bits)
	this layer includes routers.
Address Resolution Protocol links IP and MAC addresses.

Example

- binary data, added a L3 header to it, added a L2 header to it. Sent it (NOT SURE HOW WE MADE THE DECISION OF WHICH HOST/ROUTER TO SEND IT TO). 
- Removed L2 header, added new one and sent it out again.
- When receiving device had the same IP address as destination in L3 header, we removed L3 header.

4.
5.
6.
7.

## Open Questions
- IPv4 vs IPv6
- dynamic vs static ip
- Subnetting
- Can there be > 1 gateway for any host?
- Does a switch handle the case of 1 to many? A -> B and C simultaneously 
- (FROM OSI model video), does each router have multiple MAC addresses and/or NICs?
- number of devices will be different in L2 and L3 based on # of bits in MAC and IP address respectively.
- (FROM Everything a Host does video) | ARP section | How does the receiver of the broadcast verify the authenticity? Does it need to? If so, how? Similarly, how does the original sender (unicast receiver) verify the authenticity of the MAC address


New terminology: topology
