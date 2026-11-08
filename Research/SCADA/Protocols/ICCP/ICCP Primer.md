Source: Wikipedia IEC 60870-6
ICCP: Inter-control Center Communications Protocol
### Overview
ICCP provides data exchange capabilities between control centers

At a high level ICCP is responsible for the following tasks:
- Establishing and maintaining associations automatically with the remote utility sites as per its configuration
- Reporting events or alarms for remote connections 
- sending and receiving data values between control center and remote sites
- remote control and operation of local devices
- automatic initialization of transactions when the communication link is established
#### Blocks
ICCP functions are divided into blocks.
Block #1 is mandatory and allows establishing associations and exchanging data using datasets and transfer sets on a periodic basis or upon operator request.
#### Client-Server Model
##### Server
The data provider in the ICCP model provides telemetry data to one or more remote control centers. Servers accepts requests from remote clients that are verified and authenticated via associations managed by the association management function. its purpose is to establish and maintain the connections and communication sessions between client and server. Servers preform operations according to the clients request and send back the response
##### Client
The data consumer connects the the ICCP server and after succesful connection can request and recieve telemetry data. The same protocol can be used for remote commands and automation.

#### Blocks cont.
ICCP is modular by design, its different services for different types of objects are called conformance blocks or just blocks.
##### Block 1
The basic service block allows for association management and basic transfer of SCADA point data. Can be period or on request conditions
##### Block 2
The extended dataset block. Allows for reporting data value changes by exceptions? Events in DNP3?
##### Block 3
identical to block 2 but supports transfer set blocking? Allows block 1 & 2 data types be transferred as blocks instead of point by point?
##### Block 4
The information block allows sending and receiveing text or other application defined data to and from and application at a remote control center
##### Block 5
The device control block provides the selection and operation of devices
##### Block 6
Programs, used for the control of application programs on remote systems
##### Block 7
Event notification, allows a client to receive notification of events that occur on the server
##### Block 8
Allows a client to receive several different types of predefined data structures.
##### Block 9
Used for historical data

Overall block 2-9 sound like buckets for application specific behavior an implementation can provide
#### Objects and Services
objects in ICCP refer to the type of data exchanged between control centers, and services mean what type of operations are allowed to be performed on these objects and what aren't.

| Objects                   | Services                                                                                                                                                                                                                                                                                  |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Association               | A communication link between 2 control centers. The association includes the Initiate, Conclude and Abort service                                                                                                                                                                         |
| Data Values               | A data value is an object that a client can read from a server. Its usually mapped to a point in a scada database. You can get and set data values                                                                                                                                        |
| Data Sets                 | A list of data values                                                                                                                                                                                                                                                                     |
| Transfer Sets             | A transfer set defines how data may be transferred from a server to a client. For example set1 is transferred every 10 seconds and set2 is only transferred when the data inside it changes                                                                                               |
| Transfer Report           | This is the delivery mechanism for actually sending data from the server to the client. After the client has requested a start on the transfer set, the server sends transfer reports back to the client as specified by the transfer set. E.g., every 10 seconds or on other conditions. |
| Device (or Control Point) | A device that can be controlled on the remote site, or that can be controlled on the local site by the remote site                                                                                                                                                                        |
| Bilateral Table           | This is the database that defines all the associations, data values, and other objects that may be exchanged between two ICCP sites. Typically, the database contains both client and server objects.                                                                                     |