Source: DNP3 Primer Revision A
## Notes
General notes and questions

#### Terms
Master: recipient of data from multiple outstations, can also send commands
Outstation: Gather data from devices to transmit to the master
Binary signal: Data that can exist in two state: breaker is either tripped or it isn't
Analog Signal: Data that represents voltages, current, power, etc
Count input data: counters to a specific value, wrap back to 0


#### Link Layer

The link layer was established to address chunks of data from device to device. It also addresses the unreliability of the, at the time, common physical link of DNP3 devices: Serial. It is slow and unreliable, modern DNP3 is done over TCP/IP. 
Q: How is the integrity and reliability features of the DNP3 link layer utilized today if at all?

The link layer's job is data transmission, integrity, and reliability. It achieves this by:
- Framing: Wraps data in frames so that a receiver can find where a message begins. Seems redundant with TCP/IP
- Addressing: Frames cary source and destination addresses. Multiple devices can share the same connection. Seems useful
- Integrity: The CRC (cyclical redundancy check) is used to detect data corruption (checksum) Receiver can run an operation on the data it received and compare values. Same = uncorrupted. This seems slow if this is happening for every frame recieved.
- Direction and role: Each frame says where its coming from and where its going and whether its a replying or initiating an exchange.
- Reliability: Optionally a confirmed mode allows the receiver to ack each frame. Can also prevent duplicates.

#### Transport Layer

The transport layer is responsible for chunking messages into smaller packets for the link layer. Same goes on the other end, it is responsible for reassembling messages for the application layer.
"In DNP3 the transport layer is incorporated into the application layer."


#### Application Layer

The application layer should provide standardized funtions and data formatting which the user layer can interact with.
##### More terms
- Static: Represents the present value of a signal. static binary input data refers to the present on or off state of a bi-state device. One of the features of DNP3 is requesting all the static data of an outstations devices.
- Events: State changes of significance. Values exceeding thresholds. Occurs when a binary signal flips or analog signal exceeds some dead band limit. Can come with timestamps
- Classes:  A way to classify events by severity
##### Variations
DNP3 can represent data in different format, which do we use?

##### Objects
Objects are is a way to encapsulate which group and variation the data transmitted.

##### Reading data
The user layer formulates a request by telling the application layer what function to preform, and specifying what data types it wants from the outstation. This can specify specific object or a range of objects. The application layer passes the request the the transport layer to the link layer that in turn sends the message to the outstation. The link layer at the outstation then checks the frames for errors before passing it to its transport layer where the complete message is assembled by the application layer. The application layer then tells its user layer which objects were requested.
