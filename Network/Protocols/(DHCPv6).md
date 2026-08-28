The steps for DHCPv6 are:
1. The host sends an `Router Solicitation` message to the multicast address `ff02::2` to locate a DHCP router
2. The router responds with an `Router Advertisment` message
3. The host sends a DHCPv6 `SOLICIT` message to the link-local multicast address `ff02::1:2`
4. The DHCPv6 server responds with an `ADVERTISE` message
5. The host responds to the DHCPv6 server
	- **Stateless DHCPv6**: sends a `INFORMATION-REQUEST` requesting additional IPv6 configuration parameters f.e. DNS server IP address
	- **Statefull DHCPv6**: sends a `REQUEST` message to obtain all IPv6 configuration paramters
6. The DHCPv6 server  sends a `REPLY` unicast message

![[DHCPv6 steps.png|501x383]]

>[!note]
>Server to client messages use UDP port 546
>Client to server messages use UDP port 547

# Router Roles
A Cisco IOS router can be: 
- *DHCPv6 Server*: provides stateless or stateful DHCPv6
- *DHCPv6 Client*: acquires IPv6 configuration from a DHCPv6 server
- *DHCPv6 Relay Agent*: provides DHCPv6 forwarding to clients
# Stateless DHCP Operation
The stateless DHCPv6 server uses [[IPv6#Stateless Address Autoconfiguration (SLAAC)|SLAAC]] and is only providing information that is identical for all devices on the network, f.e. the subnet mask and the IP of the DNS server.

The client is sending a [[ICMPv6#RA messages|RA message]] with:
- A flag: 1
- O flag: 1
- M flag: 0

>[!note]
>This process is known as stateless DHCPv6 because the server is not maintaining any client state information (i.e., a list of available and allocated IPv6 addresses).

## Enable Stateless DHCPv6 on an Interface
#Cisco_CLI 
Stateless DHCP is enabled on a router interface using: `ipv6 nd other-config-flag` 

```
R1(config)# int g0/0/1
R1(config-if)# ipv6 nd other-config-flag
```
# Stateful DHCPv6 Operation
The RA message tells the client to obtain all addressing information from a statefull DHCPv6 server, except the default gateway address which is the source IPv6 link-local address of the RA

The client is sending a [[ICMPv6#RA messages|RA message]] with:
- A flag: 0
- O flag: 0
- M flag: 1

>[!note]
>It is called *stateful* because the DHCPv6 server maintains IPv6 state information.
## Enable Stateful DHCPv6 on an Interface
#Cisco_CLI 

Stateless DHCPv6 is enabled on a router interface using:
- `ipv6 nd managed-config-flag` 
-  `ipv6 nd prefix default no-autoconfig`

```
R1(config)# int g0/0/1
R1(config-if)# ipv6 nd managed-config-flag
R1(config-if)# ipv6 nd prefix default no-autoconfig
R1(config-if)# end
```
# Configure DHCPv6 
#Cisco_CLI 
## Stateless DHCPv6
### Stateless DHCPv6 Server
1. **Enable IPv6 routing**
   `R1(config)# ipv6 unicast-routing`

2. **Define a DHCPv6 pool name**
   `R1(config)# ipv6 dhcp pool poolName`

3. **Configure the DHCPv6 pool**
   Configure additional information including DNS server address and domain name
   `R1(config-dhcpv6)# dns-server 2001:db8:acad:1::254`
   `R1(config-dhcpv6)# domain-name example.com`
4. **Bind the DHCPv6 pool to an interface**
   `R1(config-if)# ipv6 dhcp server poolName`

   The `O` flag needs to be manually changed from `0` to `1`:
   `R1(config-if)# ipv6 nd other-config-flag `
   
```
R1(config)# interface GigabitEthernet0/0/1
R1(config-if)# description Link to LAN
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64

-> R1(config-if)# ipv6 nd other-config-flag 
-> R1(config-if)# ipv6 dhcp server IPV6-STATELESS 

R1(config-if)# no shut
```

### Stateless DHCPv6 Client
1. **Enable IPv6 routing**
   `R1(config)# ipv6 unicast-routing`
2.  **Configure client router to create an link-local address**
   `R1(config-if)# ipv6 enable`
   
```
R1(config)# interface g0/0/1
R1(config-if)# ipv6 enable
```
3. **Configure client router to use SLAAC**
   `R1(config-if)# ipv6 address autoconfig`
4. **Verify client router is assigned a GUA**
   `R1# show ipv6 interface brief`

## Stateful DHCPv6
### Stateful DHCPv6 Server
1. Enable IPv6 routing
  ` R1(config)# ipv6 unicast-routing`

2. Define a DHCPv6 pool name
   `R1(config)# ipv6 dhcp pool poolName`

3. Configure the DHCPv6 pool
   stateful DHCPv6, all addressing and other configuration parameters must be assigned by the DHCPv6 server 
   `R1(config-dhcpv6)# address prefix prefixAddress/prefix`
   `R1(config-dhcpv6)# dns-server dnsAddress`
   `R1(config-dhcpv6)# domain-name domainName`

```
R1(config-dhcpv6)# address prefix 2001:db8:acad:1::/64
R1(config-dhcpv6)# dns-server 2001:4860:4860:8888
R1(config-dhcpv6)# domain-name example.com
```
4. Bind the pool to an interface
	- The M flag is manually changed from 0 to 1: `ipv6 nd managed-config-flag`.
	- The A flag is manually changed from 1 to 0:  `ipv6 nd prefix default no-autoconfig`
	-  Bind the DHCPv6 pool to the interface: `ipv6 dhcp server poolName`

> [!NOTE]
> The A flag can be left at 1, but some client operating systems such as Windows will create a GUA using SLAAC and get a GUA from the stateful DHCPv6 server. Setting the A flag to 0 tells the client not to use SLAAC to create a GUA.

```
R1(config)# interface GigabitEthernet0/0/1
R1(config-if)# description Link to LAN
R1(config-if)# ipv6 address fe80::1 link-local
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64

-> R1(config-if)# ipv6 nd managed-config-flag
-> R1(config-if)# ipv6 nd prefix default no-autoconfig
-> R1(config-if)# ipv6 dhcp server IPV6-STATEFUL

R1(config-if)# no shut
```

### Stateful DHCP6 Client
1. Enable IPv6 routing
   `R1(config)# ipv6 unicast-routing`
2. Configure client router to create an LLA
   `R1(config-if)# ipv6 enable`

```
R1(config)# interface g0/0/1
R1(config-if)# ipv6 enable
```
3. Configure client router to use DHCPv6
   `R1(config-if)# ipv6 address dhcp`
4. Verify client router is assigned a GUA
   `R1# show ipv6 interface brief`
5. Step 5. Verify client router received other DHCPv6 information.
   `R1# show ipv6 dhcp interface g0/0/1`
## DHCPv6 Server Verification Commands
- Verify the DHCPv6 pool name and its parameters: `show ipv6 dhcp pool`
- Display the IPv6 link-local address and the GUA of the client: ` show ipv6 dhcp binding`
## DHCPv6 Relay Agent
If the DHCPv6 server is located on a different network than the client, the router can be configured as a DHCPv6 relay agent.

Configure the router: `ipv6 dhcp relay destination ipAddress portID
```
R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ipv6 dhcp relay destination 2001:db8:acad:1::2 G0/0/0
R1(config-if)# exit
```

### Verify the DHCPv6 Relay Agent
- Verify that the interface is in relay mode: `show ipv6 dhcp interface`
- Verify if any hosts have been assigned an IPv6 configuration: `show ipv6 dhcp binding`
- On the client PCs verify that it has received an IPV6 configuration from the DHCPv6 server:
  `ipconfig /all`
