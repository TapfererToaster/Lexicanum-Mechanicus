Clients have only one [[(OSI) Open Systems Interconnection-Modell#Default Gateway|Default Gateway]] configured, if it fails the client will not be able to reach other networks. The *First Hop Redundancy Protocol (FHRP)* provides redundancy and prevent this single point of failure by enabling multiple routers to be connected to the same VLAN.

# Variants
- *Hot Standby Router Protocol (HSRP)*: Cisco-proprietary, IPv4, designed for transparent failover and providing high network availability
- *HSRP for IPv6*: Cisco-proprietary, IPv6
- *Virtual Router Redundancy Protocol version 2 (VRRPv2)*: non-proprietary, IPv4, allows multiple routers on a mulitaccess link to share one virtual IPv4 address
- *VRRPv3*: non-proprietary, IPv4 + IPv6, more scaleable than VRRPv2
- *Gateway Load Balancing Protocol (GLBP)*: Cisco-proprietary, IPv4, allows for router redundancy and load balancing between multiple routers
- *GLBP for IPv6*: Cisco-proprietary, IPv6
- *ICMP Router Discovery Protocol (IRDP)*: legacy protocol, specified in RFC 1256, IPv4

# Virtual Router
Multiple routers are configured as one virtual router by sharing an IP address and a MAC address, which allows for router redundancy.
![[Virtual Router.png|515x369]]
When the active router fails the redundancy protocol changes the standby router to the new forwarding router without the disrupting the host devices connection.
![[Forwarding router fails.png|523x377]]
The following steps happen:
1. The standby router stops receiving Hello messages from the forwarding router
2. The standby router takes the role of forwarding router and assumes the IP and MAC address of the virtual router

# Hot Standby Router Protocol
HSRP is a Cisco-proprietary FHRP protocol.
## Priority and Preemption
>[!note]
>By default the router with the numerically highest IPv4 address is elected as the active router, however it is adviced to manually configure the routers.

### Priority
The router with the highest priority is the active *forwarding router*, if priorities are equal the router with the numerical highest IPv4 address is elected as active router.
The default priority is 100 and the priority range is from 0 to 255. 

Assign a priority to a router interface: `R1(config-if)# standby 1 priority priorityValue`
### Preemption
The active router will remain in this role even if another router with a higher priority comes online. Preemption is the ability to trigger a re-election process, when a router with a higher priority comes online, so it can assume the role of active router.

Enable preemption on a router interface: `R1(config-if)# standby 1 preempt`
## States and Timers
- *Initial*: The state is entered through a configuration change or when an interface first becomes available
- *Learn*: Router has not determined the virtual IP address and has not yet received a `hello` message from the active router; the router waits for a message from the active router
- *Listen*: the router knows the virtual IP address, but is not the active or standby router; it listens for `hello` messages from these routers
- *Speak*: The router sends hello messages and actively participates in the election of the active and/or standby router
- *Standby*: The router is a candidate to become the next active router and sends periodic `hello` messages
- *Active*; the router is the active router

>[!note]
>By default every 3 seconds the active and standby routers send `hello` messages to the HSRP multicast address and if the standby router does not receive a `hello` message after 10 seconds it will assume the role of the active router
>The settings can be altered, although it is not advised to set the hello timer below 1 second and the hold timer below 4 seconds.


# Configuration
1. Specify the HSRP version:
   `R1(config-if)# standby version 2`
2. Configure the IP address of the virtual router
   `R1(config-if)# standby 1 ip ipAddress`
3. Set the priority of the physical router
   `R1(config-if)# standby 1 priority priorityValue`

To 