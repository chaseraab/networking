https://www.youtube.com/watch?v=xdQ9sgpkrX8&list=PLW8bTPfXNGdAZIKv-y9v_XLXtEqrPtntm&index=2

* Why is TCP such a critical protocol to understand?
* Core TCP concepts
    * TCP handshake and options
    * TCP Windows
    * TCP Retransmissions
    * Selective Acknowledgements
* Tips for isloating performance issues

Why is TCP a big deal?
    Important stuff uses it for now
    Handles loss and congestion well

[OSI Model](https://aws.amazon.com/what-is/osi-model/#:~:text=The%20Open%20Systems%20Interconnection%20(OSI,across%20geographical%20and%20political%20boundaries.))
Application
Presentation
Session
Transport
Network
Data Link
Physical

# How does TCP start its conversation?

Additional Resources
* https://www.geeksforgeeks.org/computer-networks/tcp-3-way-handshake-process/

The handshake used to establish a reliable connection between a client and a server before data transmission begins. The handshake ensures both parties are synchronized and ready for commincation.

* https://madpackets.com/2018/04/25/tcp-sequence-and-acknowledgement-numbers-explained/

Explanation of sequence and acknowlegement numbers.

## TCP Segment Structure
A TCP segment consists of a header and data.

<img title="TCP segment" src="images/TCPSegmentHeader.jpg">

### Header
- ranges from 20-60 bytes
- 40 bytes are for options
- Fields:
    - Source port address: port address of the sender
    - Destination oport address: port address of the receiver
    - [Sequence number](https://www.geeksforgeeks.org/computer-networks/wrap-around-concept-and-tcp-sequence-number/): Used to reassemble the message at the receiving end to ensure the correct order
    - Acknowledgement number: byte number that the receiver expects to receive next.
    - Header Length: indicates the length of the TCP header (length is calculated by the number * 4 (since its 4-bit) so a length of 20 bytes is 5)
    - Control flags

## The TCP handshake
- Client wants to talk to a server, before that it needs the handshake
- TCP SYN (client to server)
    - SYN is called such since a synchronization between server and client in terms of sequence and acknowledgemnet numbers
- SYN / ACK (server to client)
- ACK (client to server)

<img title="TCP handshake" src="images/TCP-Handshake.jpg">

# TCP Attributes
- Sequence numbers
    keeps track of packets in a conversation
    Sent by the client
    Wireshark will show 0 (relative sequence number)
        The hex will show a much longer number
- Acknowledgement number
    Also a 4 byte number
    Starts at 0
    The ack number is sent by the server
- Window size value
    The size of a message I'm willing to accept
- TCP Options
    Ground rules in the relationship
    Maximum segment size
        Packet size
    No-Operation
    SACK permitted
        These options are used to pad the header to make the appropriate header length (indicated by the Header Length field)
    Window Scale
        True receive window - allows the two parties to confirm what size message they can send and receive
        This is essentially a bandaid ontop of limitations by the original design of TCP
- Calculated window size = Window * Window size scaling factor
    
- IP Header
    Time to live
        Where the point of capture was
        It indicates the number of hops
        This number will decrement with each router it hops over