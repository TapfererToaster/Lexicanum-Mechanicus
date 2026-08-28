#CCNA 

Ethernet is a [[Network Concepts & Basics#Local Area Network (LAN)|LAN]] technology, which uses [[Cables, Connectors and Ports#Copper Twisted-Pair Connections|twisted-pair]] ,[[Cables, Connectors and Ports#Fiber-optic connections| fiber-optics]] and coaxial cables.
It operates in the [[(OSI) Open Systems Interconnection-Modell#2. Datensicherungsschicht (Data Link, Layer 2)|data link]] and the [[(OSI) Open Systems Interconnection-Modell#1. Physische Schicht (Physical, Layer 1)|physical layer]] of the OSI-Model and is defined in the IEEE 802.2 and 802.3 standards.
# Sublayers
![[Data-link Ethernet MAC sublayer.png]]
Ethernet operates on the [[(OSI) Open Systems Interconnection-Modell#Media Access Control (MAC) Sublayer|MAC Sublayer]] of the data link layer, which is responsible for data encapsulation and accessing the media.

## Data Encapsulation
[IEEE 802.3](https://en.wikipedia.org/wiki/IEEE_802.3) data encapsulation includes the following:
- **Ethernet frame**:
   Internal structure of the Ethernet frame, fields within the frame are delimited by delimiting bits that provide synchronization between the transmitting and receiving nodes 
- **Ethernet Addressing**:
   The frame includes a source and destination MAC address to deliver the Ethernet frame from one Ethernet NIC to another Ethernet NIC on the same LAN
- **Ethernet Error detection**: 
  The frame includes a *frame check sequence (FCS)* trailer for error detection

## Media Standards
IEEE 802.3 also includes the specification (speed, cable types and distances) of different Ethernet communications standards over different media (copper, fibre, ...).
- IEEE 802.3u Fast Ethernet
- IEEE 802.3z Gigabit Ethernet over Fiber
- IEEE 802.3ab Gigabit Ethernet over Copper
- IEEE 802.3ae 10 Gigabit Ethernet over Fiber

>[!note]
>Legacy Ethernet using a bus topology or hubs, is a shared, half-duplex medium,  which uses *[[(OSI) Open Systems Interconnection-Modell#Carrier sense multiple access with collision detection (CSMA/CD)|carrier sense multiple access with collision detection]]*. 
>Modern Ethernet LANs use switches that operate in full-duplex and do not require access control through CSMA/CD.
### Standards for TP-cables
Ethernet also uses various standards for [[Cables, Connectors and Ports#Copper Twisted-Pair Connections|TP cabling]], some of them are:
![[TP-Ethernet Standards.png]]

| Speed    | Speed-derived<br>Name         | IEEE task Group | Informal Name | Cable Cat |
| -------- | ----------------------------- | --------------- | ------------- | --------- |
| 10 Mbps  | Ethernet                      | IEEE 802.3i     | 10Base-T      | Cat 3     |
| 100 Mbps | Fast Ethernet                 | IEEE 802.3u     | 100Base-T     | Cat 5     |
| 1 Gbps   | Gigabit Ethernet (GbE)        | IEEE 802.3ab    | 1000Base-T    | Cat 5e    |
| 10 Gbps  | 10 Gigabit Ethernet (10GbE)   | IEEE 802.3an    | 10GBase-T     | Cat 6a    |
| 100 Gbps | 100 Gigabit Ethernet (100GbE) |                 |               |           |

**Ethernet**

| Informal Name | Speed   | IEEE task Group | Cable | Reach  | Cable type |
| ------------- | ------- | --------------- | ----- | ------ | ---------- |
| 10Base-T      | 10 Mb/s | IEEE 802.3i     | Cat 3 | 100 m  | TP         |
| 10Base-F      | 10 Mb/s | IEEE 802.3j     |       | 1000 m | Fiber      |
**Fast Ethernet**

| Informal Name | Speed    | IEEE task Group | Cable | Reach  | Cable type |
| ------------- | -------- | --------------- | ----- | ------ | ---------- |
| 100Base-T     | 100 Mb/s | IEEE 802.3u     | Cat 5 | 100 m  | TP         |
| 100Base-FX    | 100 Mb/s | IEEE 802.3u     |       | 2000 m | Fiber      |
**Gigabit-Ethernet (GbE)**

| Informal Name | Speed    | IEEE task Group | Cable      | Reach | Cable type |
| ------------- | -------- | --------------- | ---------- | ----- | ---------- |
| 1000Base-TX   | 1 Gb/s   | IEEE 802.3ab    | Cat 5e     | 100 m | TP         |
| 2,5GBase-T    | 2,5 Gb/s | IEEE 802.3bz    | Cat 5e     | 100 m | TP         |
| 5GBase-T      | 5 Gb/s   | IEEE 802.3bz    | Cat 6      | 100 m |            |
| 1000Base-SX   | 1 Gb/s   | IEEE 802.3z     | Multimode  | 550 m | Fiber      |
| 1000Base-LX   | 1 Gb/s   | IEEE 802.3z     | Singlemode | 10 km | Fiber      |
| 1000Base-ZX   | 1 Gb/s   |                 | Singlemode | 70 km | Fiber      |
**10-Gigabit-Ethernet (10GbE)**

| Informal Name               | Speed   | IEEE task Group | Cable      | Reach | Cable Type |
| --------------------------- | ------- | --------------- | ---------- | ----- | ---------- |
| 10GBase-T                   | 10 Gb/s | IEEE 802.3an    | Cat 6a     | 100 m | TP         |
| 10GBase-SR<br>(Short Reach) | 10 Gb/s | IEEE 802.3ae    | Multimode  | 300 m | Fiber      |
| 10GBase-LR<br>(Long Reach)  | 10 Gb/s | IEEE 802.3ae    | Singlemode | 10 km | Fiber      |

>[!note]
>The different names names of the standards are derived from 
> - the maximum supported transmission speed
> - the name of the [[Organizations#Institute of Electrical and Electronics Engineers (IEEE)|IEEE]] task group that defined the it
> - an informal name by the IEEE that indicates the speed and cable type (standards for copper cable end with T)
> - name of the cable standard as defined by Telecommunications Industry Association (TIA) and Electronic Industries Alliance (EIA), as the cables themselves are not defined, but only used by the IEEE

**100-Gigabit-Ethernet (100GbE)**

| Informal Name | Speed    | IEEE Task Group | Cable      | Reach | Cable Type |
| ------------- | -------- | --------------- | ---------- | ----- | ---------- |
| 100GBase-CR10 | 100 Gb/s | IEEE 802.3bj    |            | 7 m   | Twinaxial  |
| 100GBase-SR4  | 100 Gb/s | IEEE 802.3ba    | Multimode  | 100 m | Fiber      |
| 100GBase-SR10 | 100 Gb/s | IEEE 802.3ba    | Multimode  | 100 m | Fiber      |
| 100GBase-LR4  | 100 Gb/s | IEEE 802.3ba    | Singlemode | 10 km | Fiber      |
| 100GBase-ER4  | 100 Gb/s | IEEE 802.3ba    | Singlemode | 40 km | Fiber      |
**Terabit Ethernet (TbE)**

| Informal Name | Speed    | IEEE Task Group | Cable      | Reach | Cable Type |
| ------------- | -------- | --------------- | ---------- | ----- | ---------- |
| 200GBase-DR4  | 200 Gb/s | IEEE 802.3bs    | Singlemode | 500 m | Fiber      |
| 200GBase-FR4  | 200 Gb/s | IEEE 802.3bs    | Singlemode | 2 km  | Fiber      |
| 200GBase-LR4  | 200 Gb/s | IEEE 802.3bs    | Singlemode | 10 km | Fiber      |
| 400GBase-FR8  | 400 Gb/s | IEEE 802.3bs    | Singlemode | 2 km  | Fiber      |
| 400GBase-LR8  | 400 Gb/s | IEEE 802.3bs    | Singlemode | 10 km | Fiber      |
| 400GBase-SR16 | 400 Gb/s | IEEE 802.3bs    | Multimode  | 100 m | Fiber      |
| 400GBase-DR4  | 400 Gb/s | IEEE 802.3bs    | Singlemode | 500 m | Fiber      |
# Frames 
Ethernet frames have a minimum size of 64 bytes and an expected maximum of 1518 bytes, including the destination MAC address field through the check sequence (FCS). 
If the size of a frame it less than the minimum or greater than the maximum, the receiver drops the frame and considers it invalid. 
Frames, which are less than 64 bytes in length are considered "collision fragments" or "runt frames", frames with more than 1500 bytes of data are considered "jumbo" or "baby giant frames".

>[!important]
>The preamble field is not included when describing the size of the frame.
>When additional requirements are included, such as [[(VLAN) Virtual LAN#VLAN Tagging|VLAN tagging]] the frame size may be larger.

## Header and Trailer
![[Ethernet Header and Trailer.png]]
### Preamble and Start Frame Delimiter (SFD)
>[!note]
The *Preamble* and the *Start Frame Delimiter (SFD)* are not part of the Ethernet frame but are sent with each frame.
>They are not considered part of the Ethernet frame, as they are a function of Layer 1, which does not contain Layer 2 data.

The Preamble and SFD allows the NIC of the receiving device to synchronize its *receiver clock*. The clock is used to determine the precise length of 1 bit.
- The *Preamble* is 7 bytes (56 bits) long an is a series of alternating 1 and 0 (f.e. 10101010).
- The *SFD* is 1 byte in length and has the bit pattern 10101011. It signals that the Preamble is finished and the frame is going to start.
### Destination and Source
These fields contain the destination and source [[(OSI) Open Systems Interconnection-Modell#2. Datensicherungsschicht (Data Link, Layer 2)|MAC address]] and each is 6 bytes long.
- The destination address is used to forward the frame to the appropriate device.
- The source address is used by the switch to learn which port each host is connected to. 
### Type/Length
This field is 2-bytes long and is used to either indicate the *type* ([[IPv4]] or [[IPv6]]) or the length of the packet.
There are historical reasons why this field can be used for either of the two, but today it is usually used to indicate the type.

>[!note]
>In the original IEEE 802.3 standard this field was exclusively used to indicate the length of the encapsulated packet. To indicate the type of encapsulated protocol the *Logical Link Control (LLC)* header was used, sometimes with an additional *Subnet Access Protocol (SNAP)* extension to the header.

A value of 1500 (decimal) or less indicates the length of the encapsulated protocol, f.e. a value of 1300 means the encapsulated packet is 1300 bytes in length.
When the field is used to indicate the type, the field is called *EtherType*.
A value of 1536 or greater indicates the type of encapsulated packet:
- IPv4: 0x0800 (0d2048)
- IPv6: 0x86DD (0d34525)

>[!warning]
>Values between 1500 and 1536 should not be used in this field.

### Frame Check Sequence
The *Frame Check Sequence* is the only field in the Ethernet trailer and is 4 bytes long.
It is responsible to detect corrupted data in a frame by using a *Cyclic Redundancy Check (CRC)*. This is done by calculating a *checksum* before the frame is send. The receiving device can then compute its own checksum and compares the two. If the two checksums are not identical the frame is discarded, as it means that the data has been corrupted during transportation.
