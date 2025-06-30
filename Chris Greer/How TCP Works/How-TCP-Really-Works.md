# The Handshake
https://www.youtube.com/watch?v=HCHFX5O1IaQ&list=PLW8bTPfXNGdAZIKv-y9v_XLXtEqrPtntm&index=3

How TCP connections are initiated

## SYN
The TCP SYN is the initiation of the TCP handshake

Wireshark tip
- Filter conversation to TCP to better get an idea of TCP communication

Stream index
- Assigned by wireshark
- Each connection has its own stream index

Sequence number indicates the sequence of the conversation

Maximum segment size: The packet size I'm willing to accept
- Routers along the path can change this
Window scale scales the size of the TCP window

Maximum Segment Size vs TCP Window Size:

    The Maximum Segment Size is the largest TCP segment that can be transported in a single IP packet. It is derived from the Maximum Transfer Unit (MTU) minus IP header overhead minus TCP header overhead. For TCP over IPv4 over Ethernet without options, that's 1460 bytes.

    The TCP window size is the amount of data "in flight", ie. being transmitted before an ACK is required. The window size depends on the channel, especially its available bandwidth and its round-trip time (RTT). The window size is adapted constantly to avoid congestion. Normally, it's a multiple of the MSS.

    MSS and window size are completely different things and pretty much independent of each other.

The point of the SYN is to start the conversation
    Provides initial sequence number
    Provides parameters for the TCP conversation

## SYN Ack
Provides an Acknowledgement number of 1
- "Ghost byte"
Flags
- Syn and Acknowledgement flags are set

## Ack
The final packet in the handshake
Sequence number is 1
Acknowledgement number is 1
Will confirm attributes of the conversation based on both parties preferences 
- i.e. final Calculated window size

# Window Scaling
https://www.youtube.com/watch?v=2PJVHvthrNU&list=PLW8bTPfXNGdAZIKv-y9v_XLXtEqrPtntm&index=7

Window size vs Calculated window size
Window size is sender indicating how much TCP buffer it has allocated remaining for this connection
In order to have a larger Window size, Window scaling is used
Calcualated Window Size = Window size * window scaling

The client and server both set their preferences on the matter
    Client is typically larger since we are typically receiving information from a server
Window scaling can go up to 14
Calculated Window size can decrease overtime as the client fills up with information and not processing it and removing it from the buffer
If the CWS hits 0, the client buffer is full and the server will stop sending data

# MTU vs MSS
https://www.youtube.com/watch?v=XMcYwr-yJGA&list=PLW8bTPfXNGdAZIKv-y9v_XLXtEqrPtntm&index=4

## MTU
MTU = Maximum Transmission Unit
How large will the data in the ethernet frame be?
MTUs are set locally and not aware of the counterpartys' MTU

MTU mismatch
- When one communicator is higher than the other

IP MTU
- Maximum transmission unit for an IP packet

## MSS
Maximum segment size
Set at the TCP level

# Sequence Numbers
https://www.youtube.com/watch?v=BWILgDt6jz0&list=PLW8bTPfXNGdAZIKv-y9v_XLXtEqrPtntm&index=6

Wireshark provides a relative sequence number, which is 0. 
After the handshake occurs the client will send data to the server
The amount of data sent is tracked by the TCP segement length.
The current sequence number + the TCP segment length = the next sequence number.
Each party will maintain its own sequence number

Wireshark will let you know if a sequence number was missed

# Acknowledgement Numbers
https://www.youtube.com/watch?v=AX2D_n1yZko&list=PLW8bTPfXNGdAZIKv-y9v_XLXtEqrPtntm&index=12

An acknowledgement of where the system is in processing the information provided by a counterparty.
    "I'm currently at this sequence number"

Wireshark will show a checkmark in the packet list indicating which packet is being acknowledged

# Selective Acknowledgement (SACK)
https://www.youtube.com/watch?v=VERgI8QaYPY&list=PLW8bTPfXNGdAZIKv-y9v_XLXtEqrPtntm&index=13

Additional docs:
https://www.geeksforgeeks.org/computer-networks/selective-acknowledgments-sack-in-tcp/


An option that is sent by a party to indicate the loss of a packet
In wireshark this is indicated by  TCP Previous segment not captured


