#Datacenter 

Zoning is used to control access between storage devices or user groups in a fabric

**Zone**
- A zone consists of multiple zone members, with each member in a zone being able to access each other but not members of other zones
- If zoning is not activated all devices are members of the default zone
- Devices can belong to multiple zone

**Zone Set**
- Consists of one or multiple zones
- can be activated or deactivated across all switches in a fabric
- only on zone set can be active at a time
- zones can belong to one or multiple zone sets

**Zone Members**
Membership of a zone can be assigned by:

>[!note]
>[[Fibre Channel#Addressing|WWN and FCID]]

- **Ports World Wide Name (pWWN)**: 
  specifies the pWWN of a N port attached to the switch
- **Fabric pWWN**:
  specifies the WWN of the fabric port; also known as port-based zoning
- **FCID**:
  specified the FCID of an N port 
- **Interface and switch WWN (sWWN)**:
  specifies the interface of a switch; also known as interface-based zoning
- **Interface and domain ID**:
  specifies the interface of a switch identified by the domain ID
- **IPv4 address**:
  specifies the IPv4 address and subnetmask of a device
- **IPv6 address**:
  specifies the IPv6 address of a device
- **Nodename**:
  specifies the name of a node

>[!note]
>For a zone with n members, n*(n-1) access permissions need to be enabled.

It is best practice to avoid configuring a large number of targets or initiators in a zone, as this will waste switch resources to manage initiator-to-initiator or target-to-target pairs that will never communicate. 

When creating zone members the following should be considered:
- one initiator and one target for a zone is the most efficient configuration for switch resources
- Configuring the same initiator for multiple targets is valid
- Configuring multiple initiators to multiple targets is not recommended

# Zoning Enforcement
Each end device (N port) discovers other devices in the fabric by querying the name server, which returns a list of all devices that can be accessed, after the a log in.
**Soft zoning**:
- zoning restrictions are applied only to interactions between the name server and end devices, if an end device knows the FCID of a device it can access it.
- only the control plane is policed 
- FC Name Server limits the list of permitted devices in an FCNS reply to those devices that are in the zone configuration
- end device data plane is is unpoliced, rogue end devices can connect to other devices they are not zoned with

**Hard zoning**:
- zoning is enforced by the hardware on each frame sent from an N port, by comparing the source-destination IDs with the permitted combinations 
- is applied to all forms of zoning and is enforced on every frame to prevent unauthorized access
- the control and data plane traffic are policed
- Control plane traffic is policed by the switch 
- Data plane traffic is policed on each ingress port with hardware assistance
- the destination of each frame is checked and if it is not in the right zone the frame is dropped
- Policy rules are programmed into each port

# Zone Sets
