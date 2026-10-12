#Datacenter 

A VSAN is a virtual SAN isolating and grouping devices that are connected to the same fabric, allowing the creation of multiple logical SANs over one physical SAN
Each VSAN contains its own Fibre Channel fabric services.

# Attributes

**VSAN ID**
identifies the VSAN 
default VSAN (VSAN 1), user defined VSANs (VSAN 2 - 4093) and isolated VSAN (VSAN 4094)

**State**
administrative state of the VSAN
- active: VSAN is configured and enabled
- suspended: VSAN is configured but not enabled

**VSAN name**
Text string (1-32 characters long) that identifies the VSAN and must be unique across all VSANS

**Load-balancing attributes**
Indicate the use of the *source-destination ID (src-dst-id)* or by default the *originator exchange OX ID (src-dest-ox-id)* for load balancing path selection


# Trunking
Trunking enables ports to transport frames from more than one VSAN.
Trunking is supported on E and F ports, as well as on native and virtual Fibre Channel interfaces.

Trunking can only be configured on E ports, which when enabled is referred to as an TE port.