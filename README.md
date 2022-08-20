# TCP or UDP

Any client-server communication will usually happen over HTTP or HTTPS channels, and in case the communication is bidirectional we will use web socket protocols.

**In TCP,** the connection is formed after a three-way TCP handshake i.e. client sends a connection request to the server, the server responds with an acknowledgment, the client responds back with an acknowledgment of the acknowledgment and a connection is formed. This 3-step process is known as a **three-way TCP handshake**.

##### Data transfer in TCP
A point to remember here is that TCP is a **lossless protocol**.  
That means the data packets cannot go missing.  
TCP ensures this by receiving an acknowledgment from the receiver for **every data packet** it receives.  
Until the sender receives the acknowledgment for a data packet it will keep sending the data packet again and again

Another thing TCP does is **congestion control** i.e. every time the network gets choked due to high traffic, it will delay sending some data packets so as to not overwhelm the network. 

So including the time taken for a handshake, acknowledgments from the server, resending of the same packets, and delay introduced because of congestion control, there is a lot of overhead involved to maintain data accuracy which might not be a priority in each use case


**UDP** is different from TCP in that it is a **lossy protocol**.

Unlike TCP, in UDP there is no requirement to form a connection. 
As long as the devices are aware of each other’s public IP address, they can talk via peer to peer connection. 

Also, as mentioned above, UDP is a lossy protocol, which means there is no concept of acknowledgment in UDP. If the sender sends packets P1, P2, P3, and P4 but the receiver only receives packets P1, P3, and P4, the sender won’t bother sending P2 again i.e. there might be some data loss.

So using UDP means less congestion since extra traffic is avoided and one packet is sent only once, less data transfer since we can avoid all those acknowledgments and lesser header size. So though the data reaching the receiver might not be perfect, it will reach a lot faster.

### Which to use
* For a chat system, we must use TCP since we can't afford to loose message in between.
* However, for a video call, just UDP will be enough.
* For a system like zoom, we will be using a combination of TCP and UDP. All the API calls, all communication between components, etc will happen over TCP but all video transfer will happen over UDP.