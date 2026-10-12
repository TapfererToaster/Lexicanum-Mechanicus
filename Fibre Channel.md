#Datacenter
https://en.wikipedia.org/wiki/Fibre_Channel

Fibre Channel is a protocol for high speed data transfer, providing in-order lossless delivery of raw block data.

# Port Types
Fibre Channel Ports can be configured as a *downlink*. that is connected to a server, or as an *uplink*, that is connected to the SAN.
Each physical interface can configured to operate as one mode.

**Extension Port**
*E ports* , can be connected to other E ports to create an inter-switch link, to carry frames for configurations and fabric management to remote N ports.

**Fabric Port**  
A *F port* can only be attached to a N port, connected to a peripheral device (host or disk)

**Node Port**
A *N port* is usually connected to a F port on a switch or another N port.

**Node Proxy Port**
A *NP port* is used on ports that function in *Node-Port-Virtualization (NPV)* mode and are connected to a F port on a core switch. This port functions as a proxy for multiple physical N ports.

**Trunking Extension Port**
A *TE port* can be connected to other TE ports to create an *extended inter switch link (EISL)*.
All frames are then transmitted in EISL format, containing VSAN information.

This is done to expand the following functions:
- VASN trunking
- Transport QoS parameters
- Fibre Channel traceroute (fctrace)

**Trunking Fabric Port**
A *FT port*  functions as a trunking expansion port, that can be connected to another TN or TNP port to carry tagged frames between a core switch and an NPV switch or host bus adapter (HBA).
TF ports support VSAN trunking and frames are transmitted in EISL frame format, containing VSAN information.

**Trunking Node Ports**
A *TNP port* functions as a trunking expansion port, that can be connected to a TF port to carry tagged frames between core NPIV switch and NPV switch.

**Fx Port**
A Fx Port can operate as a F port or a FL port, the port mode is determined during the interface initialization, which is depending on on the attached N port.
The Fx mode also prevents the interface to operate in any other mode.

**Auto Mode**
An interface in auto mode can operate as a F, E , TE or TF port.
The mode is determined during interface initialization and depends on the mode of the connected port.

# Addressing

>[!note]
>It should be avoided to compare WWNs to MAC and FCIDs to IP addresses

**World Wide Names (WWN)**
Every Fibre Channel port and note has a WWN, a 8 to 16 byte number that is assigned by the manufacturer. 
The WWN consists of a *Network Address Authority (NAA)*, the four most significant bits and the rest are a organizational unique identifier (OUI) or a company ID (CID) and vendor supplied information.
The format and length of the WWN is determined by the NAA:
- NAA = 1, 2, 5 -> 8 byte
- NAA = 6 -> 16 byte

There are two types of WWN
- *port WWN (pWWN)*
  identifies a port in a FC fabric
- *node WWN (nWWN)*
  identifies a node, f.e. switch, disk drive, in a FC fabric

**Fiber Channel Identifiers (FCID)**
A *FCID* is a 3 byte address that is assigned during fabric login, when a node connects to a fabric.
This address is used to route frames across the fabric using [[(FSPF) Fabric Shortest Path First]] protocol.
The FCID consists of three fields each 8 bits long:
- *Domain ID*:
  assigned to each FC switch in a fabric to uniquely identify it and to be used in routing decision
  The maximum number of FC switches in a fabric is restricted to 239 by this field
- *Area ID*
  this field represents a set of devices that are connected to N ports on a switch and restricts the maximum number of ports to 256
- *Port ID*
  this field identifies a specific FC object in the fabric

Some FCIDs are reserved: 

| Service                                    | Address  |
| ------------------------------------------ | -------- |
| Management Server                          | 0xFFFFFA |
| Fabric Controller                          | 0xFFFFFD |
| F Port Controller /<br>Fabric Login Server | 0xFFFFFE |
| Broadcast Address                          | 0xFFFFFF |
| N Port Controller                          | 0xFFFFF0 |
| Multicast Server                           | 0xFFFFF5 |
FCIDs can be persistent, meaning they are saved across reboots, or volatile.

# Flow Control
*Buffer-to-buffer credits (BB_credits)* are used to control the number of packages that are transmitted.
BB_credits are assigned on a per hop basis between ports when a link is brought up.
Receiver respond to port login requests form transmitter with an *acccept (ACC)* frame that contains the size and number of frame buffers.
The transmitter stores these information as BB_credits and a *buffer-to-buffer credit count (BB_credit_CNT)* value in a table.
BB_credit_CNT is decreased with every packet the transmitter sends and is increased by one when the receiver sends a *receiver ready (R_rdy)* frame.

**End-to-end credits**
End-to-end credits set the maximum number of data frames a port can send without receiving an acknowledgment frame (ACK). It is set during N port login and increased when an ACK frame is received.

# Switched Fabric Initialization
The initialization of a fabric has four steps:

**Principal Switch Selection**
The principal switch is responsible to distribute domain IDs within a fabric
It is selected based on the highest priority which can be configured or is determined by:
- *Run-time priority*:
  The lowest run-time priority 
  The default priority is 128 and can be set to a value between 0 and 254
- *Switch WWN*:
  The lowest WWN

The switch with the highest priority will become the principal switch, if multiple switches have the same priority, the switch with the lowest WWN becomes principal switch

![[principal switch initialization_domain ID distri.png|428x305]]

**Principal Fabric Initialization**
The principal switch selection has multiple phases, which begin when two switches are connected via a link:
1. *Link Initialization* phase:
   port speeds are negotiated
2. *Exchange Link Parameter (ELP)* phase:
   switch information are exchanged using the controller addresses (0xFFFFFD)
   - buffer-to-buffer credit
   - timers
   - class of service
3. *Exchange Switch Capabilities (ESC)* phase:
   neighboring fabric controller negotiate the routing protocol and recognize the vendor ID of the switch
4. *Exchange Fabric Parameters (EEP)* phase:
   the principal switch is selected

**Domain ID Distribution**
Phases:
1. *domain ID assigned (DIA)* phase
   the principal switch assigns itself a domain ID and floods DIA frames with this ID
2. *request domain identifier (RDI)* phase
   each switch in the fabric that receives the DIA frame requests a domain ID. 

A domain ID can be preferred or static.
*static domain ID*:
The switch request a specific domain ID, if it does not obtain that ID it isolates itself from the fabric. 
*preferred domain ID*:
The switch requests a specific domain ID, if it does not obtain that ID it will accept a different one

The default settings are:
- domain ID: 0
- configured type: preferred

A value of 0 can only be assigned if the preferred option is used, if no domain ID is configured the local switch sends a random ID in its request. 
Recommended is the use of static domain IDs

If a subordinate switch requests a domain:
- the local switch sends a configured ID request to the principal switch
- the principal switch assigns the requested domain ID if available or assigns another available domain ID

If the received domain ID is not within the allowed list, the requested domain ID becomes the runtime domain ID of the switch and all ports are isolated.
If the received domain ID is the same as the requested ID it becomes the runtime domain ID. 

If the received domain ID is different from the requested ID the behavior depends what mode is configured:
- static domain ID:
  the assigned domain ID is discarded, all interfaces are isolated and the configured domain ID becomes the runtime domain ID
- preferred domain ID:
  the local switch accepts the received domain ID and it becomes the runtime domain ID

**FCID Allocation**
Here N ports that log into the SAN are, by default, assigned a persistent FCID and the a dynamic entry is automatically stored in a database.
A persisten FCID that is assigned to a F port can be moved across interfaces.

**Fabric Reconfiguration**
All switches in the fabric are resynchronized to ensure the simultaneously restart a new principal switch selection phase.
A new principal switch selection phase can be triggered by:
- a switch reboot
- a build fabric (BF) frame
  can be send manually, when fabrics with nonoverlapping domains are joined or due to a link failure
- a reconfigure fabric (RCF) frame
  can be send manually or automatically when a switch is isolated

# Device Registration
![[Device Registration.png]]
After a fabric is initialized, end devices connect to the fabric register:

**Fabric login (FLOGI)**
Between a N port and F port
When a N port connects to a F port the host sends a FLOGI request to the fabric login server address, containing the node name, N port name and service parameters.
The fabric switch responds with an ACC frame and after that assigns a FCID.

**Port login (PLOGI)**
Between two N ports
A N port sends a PLOGI request to the well-known directory service address, containing the port address, port name, node name, B2B_credit and other parameters.
After the exchange of PLOGI request and parameters the nodes can establish a logical session.

**Process login (PRLI)**
PRLI happens between two process (f.e. system processes) originating from different N ports

## FLOGI and FCNS Databases
Every Fibre Channel switch maintains a FLOGI and FCNS database storing the connection between WWNs and FCIDs.

>[!note]
>The FCNS database lists devices currently logged in each VSAN
>The FLOGI database lists devices logged in to each switch

**FLOGI Database**
This database logs every end device (f.e. storage, server) that has successfully performed a fabric login and received a FCID.
The *Fibre Channel Name Service (FCNS)* is used by FC switches to share FLOGI database information with each other. 

**FCNS Database**
The FCNS database is stored in the name server running on each switch and maintains the FCNS database, containing attributes of all hosts and storage devices in each VSAN.

