https://en.wikipedia.org/wiki/Fibre_Channel

Fibre Channel is a protocol for high speed data transfer, providing in-order lossless delivery of raw block data.

# Port Types
Fibre Channel Ports can be configured as a *downlink*. that is connected to a server, or as an *uplink*, that is connected to the SAN.
Each physical interface can configured to operate as one mode.

**Extension Port**
*E ports* , can be connected to other E ports to create an inter-switch link, to carry frames for configurations and fabric management to remote N ports.

**Fabric Port**  
A *F port* can only be attacked to a N port, connected to a peripheral device (host or disk)

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

