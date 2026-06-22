## Transport Layer

### What Happens in the Transport Layer?
- Process to Process Delivery (Host A to Host B)
- Segmentation and Reassembly (It takes large chunks of data from the Application Layer and chops them into smaller manageable pieces called segment)
- Multiplexing and Demultiplexing
- Flow Control
- Error Control and Reliability

### What things are needed?
- Protocols(TCP & UDP)
- Port numbers
- Sockets
- Headers

### Characteristics of TCP
- Connection Oriented
- Reliable Service
- Full-Duplex communication

| Feature | Connection-Oriented | Connectionless |
| --- | --- | --- |
| **Initial Setup** | Required (Handshake) | Not required |
| **Reliability** | High (Guaranteed delivery) | Low (Best effort) |
| **Data Ordering** | Guaranteed in-order | Not guaranteed |
| **Speed / Delay** | Slower (due to setup & tracking) | Faster (immediate transmission) |
| **Overhead** | High | Low |
| **Analogy** | A phone call | Sending a postcard |
| **Primary Protocols** | TCP, ATM, Frame Relay | UDP, IP, ICMP |

### Services of TCP
- Process to Process, Stream delivery Service, Buffering, Multiplexing/Demultiplexing

<img src="/Diagrams/tcp-udp.svg">

### Characteristics of UDP
- Connectionless
- Unreliable
- Minimum overhead


### Services of UDP
delivering data without requiring connection setups, delivery guarantees, or packet ordering

When we talk about addressing in the Transport layer, we are talking about **Port Numbers**.

While the Network layer uses IP addresses to get a packet to the correct *device*, the Transport layer uses Port numbers to get that packet to the correct *application process* running on that device.

### How Port Addressing Works

A Port is simply a 16-bit number, meaning there are 65,536 possible ports (ranging from 0 to 65535). They are divided into three specific ranges:

**1. Well-Known Ports (0 – 1,023)**
These are globally standardized and reserved for common, critical services. You cannot usually assign these to a random application you build.

* **Port 80:** HTTP (Standard web traffic)
* **Port 443:** HTTPS (Secure web traffic)
* **Port 22:** SSH (Secure remote login)
* **Port 53:** DNS (Translating names to IP addresses)

**2. Registered Ports (1,024 – 49,151)**
These are loosely assigned by the Internet Assigned Numbers Authority (IANA) for specific applications or vendor services, but they aren't as strictly controlled as the well-known ports.

* **Port 3306:** MySQL Database
* **Port 5432:** PostgreSQL Database
* **Port 8080:** Often used for alternative web servers or proxies.

**3. Dynamic / Ephemeral Ports (49,152 – 65,535)**
These are temporary "scratchpad" ports. When you open a web browser to go to Google (Port 443), your computer needs a return address so Google knows where to send the webpage back to. Your operating system grabs a random port from this range (e.g., 50123) and assigns it to your browser tab for the duration of that specific connection. When you close the tab, the port goes back into the pool.

### The Socket Address

To create a complete, unique, end-to-end connection across the internet, the Transport layer combines the IP address (from the Network layer) with the Port number. This combination is called a **Socket Address**.

Format: `IP_Address : Port_Number`
Example: `192.168.1.15 : 443`

By using Sockets, a server can handle thousands of concurrent connections because every single connection has a mathematically unique socket pair (Client IP:Port communicating with Server IP:Port).

`Both headers start with the exact same thing: Source Port and Destination Port. No matter which protocol you use, the Transport Layer always needs to know which applications are talking to each other.`


![Header](/Transport%20Layer/Diagrams/header.svg)

## Multiplexing and Demultiplexing 

- Multiplexing : The Process of gathering data chunks from multiple different applications running on your device, attaching a specific "Source Port" and "Destination Port" to each chunk, and combining them to be sent out over a single network connection.
- Demultiplexing : The process of receiving a combined stream of traffic from the network, reading the "Destination Port" on each incoming packet, and sorting them so the data is delivered to the exact correct application 

![Multiplexing/Demultiplexing](/Diagrams/mude.svg)

## Encapsulation and Decapsulation

- Encapsulation: The process of taking data and adding a header (and sometimes a trailer) as it moves *down* the network layers for transmission.
- Decapsulation: Decapsulation refers to the removal of all these additional information and extraction of originally existing data, and this process continues till the last layer i.e. the Application Layer.

![Encapsulation/Decapsulation](/Diagrams/encap-decap.svg)

## Networking Layer versus transport layer

* **Network Layer (Device-to-Device):** Uses IP addresses to move data between physical computers. *(Getting the package to the right building).*

![Process to Process](/Transport%20Layer/Diagrams/ptop.svg)

* **Transport Layer (Process-to-Process):** Uses Port numbers (TCP/UDP) to connect specific applications running on those computers. *(Delivering the package to the exact right room).*

## Control Mechanisms

The transport layer provides end-to-end communication between devices by managing how data is packaged, sequenced and delivered. It ensures data reaches the correct application using port numbers and utilizes three primary control mechanisms: Flow Control, Error Control, and Congestion Control

### Flow Control 

Flow control ensures that the sender does not overwhelm the receiver with too much data at once. It balances the rate of transmission so that:

- The sender transport layer doesn’t flood the receiver.

- The receiver transport layer can buffer, process, and deliver data smoothly to the application process.


![Flow Control](/Transport%20Layer/Diagrams/flow.svg)

- Sender Application to Transport: The App pushes data down. If the Transport layer's memory buffer fills up, it uses a flow control signal to tell the App to pause.

- Across the Network: The Sender Transport pushes packets across the internet to the Receiver Transport. The Receiver uses network-level flow control (like TCP Window Size) to tell the Sender to throttle its speed if necessary.

- Receiver Transport to Application: The receiving App pulls the data up from the Transport layer exactly when it is ready to process it.


Based on your lecture slides, here is why each of these control mechanisms is necessary at the transport layer:



### 2. Error Control

Error control is required because the primary underlying network layer protocol, IP, is inherently unstable and unreliable.

* **The Reason:** Packets can be corrupted, lost, duplicated, or delivered out of order as they travel across the network.


* **Responsibilities:** The transport layer's error control mechanism is specifically responsible for:
* Detecting and discarding corrupted packets.


* Keeping track of lost/discarded packets and resending them.


* Recognizing and discarding duplicate packets.


* Buffering out-of-order packets until any missing packets safely arrive.


### 3. Congestion Control

Congestion control is necessary to keep the total network load below its actual capacity.

* **The Reason:** Congestion occurs across networks because intermediate network devices like routers and switches use queues (buffers) to hold packets before and after processing them. If too many packets arrive at once, these buffers overflow, causing packet loss and severe delays.
* **Connection to Network Layer:** Congestion at the transport layer is directly caused by congestion happening at the network layer. Managing this is a critical issue for maintaining overall internet performance and stability.


### TCP

![Flow Control](/Transport%20Layer/Diagrams/handshake.svg)

A SYN segment consumes one sequence number, even though it carries no data. Therefore, the Server acknowledges seq: 8000 by returning ack: 8001.  A SYN + ACK segment also consumes one sequence number. The Client acknowledges seq: 15000 by returning ack: 15001.  An ACK segment carrying no data does not consume a sequence number. Connection termination follows a similar three-way pattern utilizing the FIN flag.  