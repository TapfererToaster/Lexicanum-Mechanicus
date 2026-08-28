# The Basics of Routing
![[Routing Basic.png]]
When a router receives a frame that is addressed to its MAC address it de-encapsulates it and inspects its IP address. If the destination IP address in the packet is its own the router will continue to de-encapsulate the message as it is a message for the router itself.

If the destination IP address is not its own the router will look up the destination IP address in a routing table to find a suitable route . If one is found the packet will be forwarded to the next hop, if not the router will discard the packet 
## Routing Table
The routing table is a database of known destinations containing the routes to other networks and their network information, like address and netmask.

It can be thought of as a set of instructions: 
- To send a packet to destination X, forward it to next hop Y
- If the destination is in a directly connected network, forward the packet directly to the destination
- If the destination is the router's own IP address, do not forward the packet (continue to de-encapsulate)

>[!note]
>You can view the routing table on a Cisco router with the command `show ip route`

>[!note]
>Without any configuration the routing table will be empty.

**Default Router**
Alle Pakete deren Zielnetz unbekannt sind werden an den Default Router geleitet.
### Connected Routes
A *connected route* is a route to the network an interface is connected to. For each interface that has an IP address and is in an up/up state one connected route is automatically added to the routing table. 
A connected route will state that the network is directly connected and which interface it is connected to.

>[!note]
>A route to more than one destination address is called a *network route*. 
>Connected Routes are network routes.

### Local Routes 
A *local route* is a route to the IP address configured on the router's interface, which tells the router that a packet destined for the configured IP address is for the router itself.
To specify the IP address of the interface, a local route uses a `/32` prefix length ( all bits are set to `s`), regardless of the netmask configured on the interface.

>[!note]
>One local route is also automatically added to the routing table for each interface that has an IP address and is in an `up/up` state.

>[!note] 
>A route to a single destination IP address (a single host) is called a *host route*.

### Show routing table
#Cisco_CLI 
To display the routing table use: `R1# show ip route`

```
R1# show ip route
...
192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks 
C     192.168.1.0/24 is directly connected, GigabitEthernet0/0 
L     192.168.1.1/32 is directly connected, GigabitEthernet0/0
```

## Route selection
Router select the *most specific matching route* , when determining which route in the routing table it will use to forward a packet.
>[!info]
>- *matching route*: The packets destination IP address is part of the network specified in the route
>- *most specific*: the route with the longest prefix length

![[Route Selection.png]]
- R1 receives a frame on its G0/0 INTERFACE
- The destination MAC is its own, it de-encapsulates it 
- The packets destination IP address is 192.168.1.1
- R1 performs a routing table lookup and finds two matching routes
  192.168.1.0/24
  192.168.1.1/32
- R1 chooses the most specific route 192.168.1.1/32

>[!note] 
>Routers will not flood a packet out of all ports when there is no matching route in the routing table, instead it drops the packet.
>Here are the actions a router can make. 
>![[Router Actions.png]]

- Das Ziel ist in einem direkt angeschlossenen Netz:
  Die MAC Adresse des Ziels wird mit ARP ermittelt und weitergeleitet
- Das Ziel ist über einen benachbarten Router erreichbar:
  Der Router sucht anhand seiner *Metrik* (größte Bandbreite, geringste Kosten) nach der besten Route zum Ziel
- Es wurde keine passende Route oder Eintrag gefunden:
  Das Paket wird an den *Default-Router* , oder auch *Gateway of Last Resort*, gesendet.
- Falls es in der Reihenfolge keinen passenden Eintrag gibt, wird das Paket verworfen und eine Fehlermeldung wird gesendet
# Routing
*Routing* is also used to refer to the processes routers use to learn routes.
There are two main methods:
- *Dynamic routing*: 
  Routers use *dynamic routing protocols* to share information with each other and build their routing tables
- *Static routing*:
  An engineer/admin manually configures routes on the router

>[!remember]
>When forwarding a packet towards its destination the router must encapsulate and address it to the MAC of the *next hop*, which is the next router in the path to the destination.

![[Figure 9.7 Routing.png]]

To establish communication between two hosts, each router only needs a route to the next hop, meaning R1 does not need to know about the network between R2 and R3.  
In other words R1 does not need to know what path the packet will take after R2.

## Static Routing
### Configuring static routes
#Cisco_CLI 
#### Next-Hop Static Route
To configure a *Next-Hop Static Route* use:
- IPv4: `R1(config)# ip route destinationNetwork destinationNetmask nextHopIP`
- IPv6: `R1(config)# ipv6 route destinationNetwork/prefix nextHopIP`

```
R1(config)# ip route 172.16.1.0 255.255.255.0 172.16.2.2

(R1(config)# ipv6 unicast-routing)
R1(config)# ipv6 route 2001:db8:acad:1::/64 2001:db8:acad:2::2
```

![[Static Route next hop configuration.png]]
>[!note]
>A static route that specifies only the next-hop IP address is called a *recursive static route*
>It is recursive, because the route necessitates multiple lookups in the routing table to forward a packet:
>- lookup to ding the UP address of the next hop
>- lookup to fing which interface the next-hop is connected to

>[!note]
>R1 knows the IP address of the next-hop, but R1 needs the next-hop's MAC address. To learn it R1 must send an ARP request to the next-hop
>
#### Directly Connected Static Route
Instead of configuring the next-hop IP address of a route, you can specify the *exit interface*, which will be used to forward packets out of.
To configure this use:
- IPv4: `R1(config)# ip route destinationNetwork destinationNetmask exitInterfaceID`
- IPv6: `R1(config)# ipv6 route destinationNetwork/prefix exitInterfaceID`

```
R1(config)# ip route 192.168.3.0 255.255.255.0 g0/0 

(R1(config)# ipv6 unicast-routing)
R1(config)# ipv6 route 2001:db8:acad:1::/64 s0/1/0
```

A static route that specifies only the exit interface is called a *directly connected static route*, the reason being that the R1 will think that the destination network is directly connected to the interface. The router will then try to send packets directly to PC3 and an ARP request will be addressed to it instead of the next-hop. If the request does not reach PC3 R1 will not be able to forward packets to it.
If R2 uses *proxy ARP* it can reply on behalf of PC3 and responds to PC1's ARP request with the MAC of the connected interface. 

>[!note]
>A router will only use proxy ARP to reply to an ARP request if it has a route to the destination in its own routing table, otherwise it will ignore the request.

![[proxy ARP.png]]
>[!warning]
>The reliance of proxy ARP has some downsides:
>- on Cisco routers proxy ARP is enabled by default, but if it is disabled or the other router is not a Cisco router, the request will fail and no packets will be forwarded
>- The router will try to make a separate ARP entry for every host on the destination network, which can waste memory

#### Fully Specified Static Route
You can also configure a *fully specified static route*, which contains the exit interface and the next-hop.
To configure this use:
- IPv4: `R1(config)# ip route destinationNetwork destinationNetmask exitInterfaceID nextHopIP`
- IPv6: `R1(config)# ipv6 route destinationNetwork/prefix exitInterfaceID nextHopIP`

```
R1(config)# ip route 192.168.3.0 255.255.255.0 g0/0 192.168.12.2

(R1(config)# ipv6 unicast-routing)
R1(config)# ipv6 route 2001:db8:acad:1::/64 s0/1/0 fe80::2
```

This kind of static route has the benefit that the router will not need recursive lookups or to rely on proxy ARP. In reality there is no noticeable difference in performance between recursive and full specified static routes.
### Configuring a Static Default Route
The *default route* is a route to the least-specific destination possible: 0.0.0.0/0, which matches all possible IP addresses, from 0.0.0.0 through 255.255.255.255 and is only used when there aren't any more specific routes. 
A default route is often used to forward packets to the internet and to the Internet Service Provider (ISP).

>[!note]
>More specific routes can be used for destinations in the internal corporate network, and then all other traffic that does not match any other routes will be routed using the defualt route.

To configure a default route use:
- IPv4: `R1(config)# ip route 0.0.0.0 0.0.0.0 {nextHopIp | exitInterfaceID}`
- IPv6: `Router(config)# ipv6 route ::/0 {nextHopIp | exitInterfaceID}` 


![[Default Route.png]]

### Floating Static Routes
Floating Static Routes are static routes that are used as a backup and is only used when the primary route is not available.
This is done by giving the floating static route a higher administrative distance, indicated by a distance value at the end of a configuration command
- IPv4: `R1(config)# ip route ... distanceValue`
- IPv6: `R1(config)# ipv6 route ... distanceValue`

```
R1(config)# ip route 0.0.0.0 0.0.0.0 10.10.10.2 5

R1(config)# ipv6 route ::/0 2001:db8:feed:10::2 5
```
### Verifying Static Routes
To verify static routes use:
- `show ip route static`
- `show ip route network`
- `show running-config | section ip route`

- Display only IPv4 Static Routes: `R1# show ip route static | begin Gateway`
- Display a specific IPv4 Network: `R1# show ip route ipAddress`
- Display the IPv4 Static Route Configuration: `R1# show running-config | section ip route`
- Display only IPv6 Static Routes: `R1# show ipv6 route static`
- Display a Specific IPv6 Network: `R1# show ipv6 route 2001:db8:cafe:2::`
- Display the IPv6 Static Route Configuration: `R1# show running-config | section ipv6 route`

### Host Routes
Host Routes are IPv4 addresses with a 32 bit mask or an IPv6 address with a 128 bit mask.
A host route can be added by:
- Automatically installed when an IP address is configured on the router
- Configured as a static host route
- automatically obtained

To configure a static host route use:
- `R1(config)# ip route hostIP 255.255.255.255 nextHopIP`
- `R1(config)# ipv6 route hostIP/128 nextHopIP`
 
```
R1(config)# ip route 209.165.200.238 255.255.255.255 198.51.100.2

R1(config)# ipv6 route 2001:db8:acad:2::238/128 2001:db8:acad:1::2
```

Configure a IPv6 static host with link-local Next-Hop:
- Remove the original static host route:
  `R1(config)# no ipv6 route 2001:db8:acad:2::238/128 2001:db8:acad:1::2`
- Configure fully specified route with the link-local address
  `Branch(config)# ipv6 route 2001:db8:acad:2::238/128 serial 0/1/0 fe80::2`
## Dynamic Routing
*Dynamic Routing* uses dynamic routing protocols for network discovery, maintaining routing tables and sharing information with other routers regarding reachability and status of remote networks.

**Interne / Externe dynamische Routingprotokolle**
*Interne Routingprotokolle* werden ausschließlich in Intranets und Autonomen Systemen eingesetzt
Hierzu gehören *Routing Information Protocol (RIP)* und *Open Shortest Path First (OSPF)*.


> [!question] Hypothese
> Wird im Intranet von ISP benutzt und um zum Externen Router zu gelangen

*Externe Routingprotokolle* werden im Internet und zwischen Autonomen Systemen verwendet.
Hierzu gehört das *Border Gateway Protocol (BGP)*.
# Troubleshooting
- `ping`: `R1# ping 192.168.2.1 source 172.16.3.1`
- `traceroute`: `R1# traceroute 192.168.2.1`
- `R1# show ip route`
- `show ip interface brief`
- `show cdp neighbors`
## Connectivity problem
- Ping the remote LAN: `R1# ping 192.168.2.1 source 172.16.3.1`
- Ping the next hop router
- Verify routing table

# Autonome Systeme 
Router in einem *Autonomen System* kennt nur andere *interne Router* innerhalb des AS. 
Für Interdomain Routing sind externe Router, Border-Router, zuständig um Kommunikation zwischen AS zu ermöglichen, und so von ISPs verwendet wird.
![[Autonome Systeme.png]]
# Routing Protokolle
## Routing Information Protocol (RIP)
RIP arbeitet nach dem Distanz-Vektor-Algorithmus, der Weg wird anhand der geringsten Anzahl der Hops zwischen Quell- und Zielnetz getroffen, wobei die maximale Anzahl an Hops 15 beträgt.
Router verschicken im 30 Sekundentakt Routinginformationen an seine Nachbarn.
Dadurch ergänzen Router ihre Routingtabellen mit Pfaden zu entfernten Netzwerken.

Versionen:
- RIPv2 ([RFC 2453](https://www.rfc-editor.org/info/rfc2453/))
- IPv6 RIPnG ([RFC 2080](https://www.rfc-editor.org/info/rfc2080/))

## Open Shortest Path First (OSPF)
OSPF basiert auf der Link State Database, in der alle benachbarten Router und deren Link-Status eingetragen sind.
Die Routinginformationen werden alle 30 Minuten  oder bei Änderungen ausgetauscht, dazwischen werden Hello Nachrichten gesendet um zu signalisieren, dass eine Verbindung besteht und es keine Änderungen gibt. Zusätzlich müssen alle Router die Routinginformationen miteinander austauschen in einem Autonomen System sein.

Der Weg wird nach den geringsten Leitungskosten ausgewählt. Je höher die Bandbreite zwischen Quell- und Zielnetz desto geringer sind die Kosten.

Versionen:
- Version 2 (RFC 2328)
- Version 3 (RFC 2740)

