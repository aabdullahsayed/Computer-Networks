### Multiplexing and Demultiplexing 

- Multiplexing : The Process of gathering data chunks from multiple different applications running on your device, attaching a specific "Source Port" and "Destination Port" to each chunk, and combining them to be sent out over a single network connection.
- Demultiplexing : The process of receiving a combined stream of traffic from the network, reading the "Destination Port" on each incoming packet, and sorting them so the data is delivered to the exact correct application 

![Multiplexing/Demultiplexing](/Diagrams/mude.svg)

### Encapsulation and Decapsulation

- Encapsulation: The process of taking data and adding a header (and sometimes a trailer) as it moves *down* the network layers for transmission.
- Decapsulation: Decapsulation refers to the removal of all these additional information and extraction of originally existing data, and this process continues till the last layer i.e. the Application Layer.

![Encapsulation/Decapsulation](/Diagrams/encap-decap.svg)
