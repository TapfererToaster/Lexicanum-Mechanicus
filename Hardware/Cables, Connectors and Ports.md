#CCNA
# Copper Twisted-Pair Connections

>[!note]
>TP cables are often called "Ethernet cables", but be aware that [[Ethernet]] is a standard that makes use of both TP and fibre-optic cables
## Connector
Twisted-Pair cables use a *8 position 8 contact (8P8C)* connector, often referred to as a *Registered Jack-45 (RJ45)* connector.
## Schirmarten
Twisted-Pair cables can have different buildups, which protect them from interference:
- *Unshielded (U)*:
  Inside the cable are only the wire pairs and no further components
  -> no protection against *electromagnetic interference (EMI)* 
- Shielded (S):
  A metallic shield, is either wrapped around all wires 
  -> protected against EMI
-  Foiled (F):
  A metallic foil is either wrapped around all wires (F/xTP) or every wire pair individually (FTP)
  -> protected against EMI
  
  >[!note] Cabling Terminology
  >To describe the type of cable we use the form *XX/YZZ*:
  >- XX: What shield is wrapped around all cables
  >- Y: What shield is wrapped around the individual wire-pairs
  >- ZZ: What type of wire-pair is used 
  > 
  >Possible cable types are:
  >- F/UTP
  >- SF/UTP
  >- U/FTP
  >- S/FTP
## Cable Types
>[!note] 
>Not all Ethernet standards use all 4 pairs of wires of the 8P8C connector.
>- 10BASE-T:       4 wires
>- 100BASE-T:     4 wires
>- 1000BASE-T:   8 wires
>- 10GBASE-T:     8 wires

### Straight-through Cables
10BASE-T and 100BASE-T use two wire pairs one for transmission and one for receiving:
*Straight-through cables* connect one pin pair to the same pins on the other device, this is used when connecting two different devices, f.e. a PC to a switch.

![[Straight-trhough wireing.png|585]]

### Crossover
*Crossover cables* are used when connecting two devices of the same type (PCs, switches, ...),  because data collision would occur, as the same pins are used for transmission or receiving. 

![[Cross-over cable.png|589]]
### Auto MDI-X
*Auto Medium-Dependent Interface Crossover (Auto MDI-X)* is a feature that allows modern devices to change the pins it uses for transmission and receiving
![[Auto MDI-X.png|593]]

>[!note] 1000BASE-T and 10GBASE-T
>  1000BASE-T and 10GBASE-T use all eight wires and every pair can be used for transmitting and receiving data simultaneously.
## Rollover
Rollover cables are used to connect a PC to the RJ45 Console port of networking devices.
![[Rollover Cable.png]]
# Fiber-optic connections
## Anatomy
Fiber-optic connections have two cables, one for transmission and one for receiving. These are connected to a *Small Form-Factor Pluggable (SFP)*, which is plugged into a SFP port on a device.
>[!note]
>When connecting two devices, the SFP transceivers have to be plugged the correct way. The transmitter must be connected to the others receiver and vice versa. 

A fiber-optic cable is made up of a glass core surrounded by multiple layers:

![[Fibre-optic anatomy.png]] 
- **1.) Glass Core**:
  very thin glass fiber, used to transport the signal
- **2.) Cladding**:
  reflective layer that helps to transport the light
- **3.) Buffer**:
  protects the inner components
- **4.) Outer jacket**:
  protects the inner components
### Multimode and Singlemode
There are two main types of fiber-optic cables
- *Multimode fiber (MMF)*:
   have a wide core and use a LED transmitter that emits light at multiple angles (*modes*), which are reflected by the cladding
- *Single-mode fiber (SMF)*
  have a thin core and use a laser transmitter that emits light at a single angle

![[SMF MMF.png]]

> [!NOTE]
> Typically SMF cables are more expensive (the Laser) and support greater maximum distances (<= 10 km) 
# TP vs. Fiber
When choosing whether to use TP or fiber cables you should consider the following points:
- maximum required distance
- cost
- what cables are supported by the devices
- what is the environment (f.e. many electrical devices)

**Fiber**:
- support greater distances
- more expensive than TP systems
- more common in network infrastructure (f.e. connecting a switch and router on different floors or buildings)
- not affected by electromagnetic interference (EMI)

**TP**: 
- cheaper
- more common in LAN infrastructure (f.e. connecting a switch with a computer)
- affected by EMI
- can leak their signal outside of the cable
