### Multiplexing and Demultiplexing 

- Multiplexing : The Process of gathering data chunks from multiple different applications running on your device, attaching a specific "Source Port" and "Destination Port" to each chunk, and combining them to be sent out over a single network connection.
- Demultiplexing : The process of receiving a combined stream of traffic from the network, reading the "Destination Port" on each incoming packet, and sorting them so the data is delivered to the exact correct application 

![Multiplexing/Demultiplexing](/Diagrams/mude.svg)

### Encapsulation and Decapsulation

- Encapsulation: The process of taking data and adding a header (and sometimes a trailer) as it moves *down* the network layers for transmission.
- Decapsulation: Decapsulation refers to the removal of all these additional information and extraction of originally existing data, and this process continues till the last layer i.e. the Application Layer.

![Encapsulation/Decapsulation](/Diagrams/encap-decap.svg)

### Networking Layer versus transport layer

* **Network Layer (Device-to-Device):** Uses IP addresses to move data between physical computers. *(Getting the package to the right building).*

![Process to Process](/Transport%20Layer/Diagrams/ptop.svg)

* **Transport Layer (Process-to-Process):** Uses Port numbers (TCP/UDP) to connect specific applications running on those computers. *(Delivering the package to the exact right room).*

### Control Mechanisms

The transport layer provides end-to-end communication between devices by managing how data is packaged, sequenced and delivered. It ensures data reaches the correct application using port numbers and utilizes three primary control mechanisms: Flow Control, Error Control, and Congestion Control

### Flow Control 
Flow control ensures that the sender does not overwhelm the receiver with too much data at once. It balances the rate of transmission so that:

- The sender transport layer doesn’t flood the receiver.

- The receiver transport layer can buffer, process, and deliver data smoothly to the application process.


![Flow Control](/Transport%20Layer/Diagrams/flow.svg)

- Sender Application to Transport: The App pushes data down. If the Transport layer's memory buffer fills up, it uses a flow control signal to tell the App to pause.

- Across the Network: The Sender Transport pushes packets across the internet to the Receiver Transport. The Receiver uses network-level flow control (like TCP Window Size) to tell the Sender to throttle its speed if necessary.

- Receiver Transport to Application: The receiving App pulls the data up from the Transport layer exactly when it is ready to process it.




