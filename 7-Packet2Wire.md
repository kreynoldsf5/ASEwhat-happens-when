# Packet Hits the "Wire"

_Context: We're trying to form our TCP connection to our HTTP destination. We're sending the previously inspected SYN packet across the internet to start that process._

_OSI Layer(s): 1-4_

At this point the packet is ready to be transmitted and hits the "wire". This could be any L1 construct -- a Cellular, Wifi, or Ethernet connection or a combination thereof. The packet will reach the router managing the local subnet and possible hop through one or more routers to eventually arrive at the Autonomous System ([AS](https://en.wikipedia.org/wiki/Autonomous_system_(Internet))) border routers -- ie. at the edge of the internet. 

AS's exchange routing information through BGP ([Border Gateway Protocol](https://en.wikipedia.org/wiki/Border_Gateway_Protocol)) to determine "where" ARIN allocated public IP blocks "live" on the internet. Ultimately, the packet will traverse other ASs (while working its way "across the internet") to arrive at the destination border router and its final destination subnet.

Each router along the way extracts the destination address from the IP header and routes it to the appropriate next hop. The time to live (TTL) field in the IP header is decremented by one for each router that passes. The packet will be dropped if the TTL field reaches zero or if the current router has no space in its queue (perhaps due to network congestion).

![Always Outdated Map of the Internet](https://upload.wikimedia.org/wikipedia/commons/c/cf/NetTransformer_Internet_BGP_map.jpg)

## TCP Connection Flow Process

* Client chooses an initial sequence number (ISN) and sends the packet to the server with the SYN bit set to indicate it is setting the ISN
* Server receives SYN and if it's in an agreeable mood:
  * Server chooses its own initial sequence number
  * Server sets SYN to indicate it is choosing its ISN
  * Server copies the (client ISN +1) to its ACK field and adds the ACK flag to indicate it is acknowledging receipt of the first packet
* Client acknowledges the connection by sending a packet:
  * Increases its own sequence number
  * Increases the receiver acknowledgment number
  * Sets ACK field

*We now have established our 3 way handshake.*
![TCP 3WH State diagram](https://cdn-images-1.medium.com/max/1306/1*n22QJMww4vGw_MrlZbysLg.png)

* Data is transferred as follows:
  * As one side sends N data bytes, it increases its SEQ by that number
  * When the other side acknowledges receipt of that packet (or a string of packets), it sends an ACK packet with the ACK value equal to the last received sequence from the other side

_Demonstration Steps:_
* Show Wireshark filter for SYNs, follow conversation to show 3WH
``tcp.flags.syn==1 && tcp.flags.ack==0``
* Show the TTL of this SYN packet

[Next: TLS Handshake](./8-TLShandshake.md)
