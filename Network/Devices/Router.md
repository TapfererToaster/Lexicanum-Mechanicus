#CCNA 

Routers are used to connect networks and the end hosts inside them to other networks and enable communication between them, f.e. the internet or multiple LANs

>[!note] Routers and home routers
>Routers are not used to connect many end hosts within a LAN.
>The wireless router usually found in homes, typically fills the roles of a router, switch and wireless access point.

Routers can be *multiprotocol* or *singleprotocol*, meaning they support only a single protocol (f.e. IPv4) or multiple protocols (f.e. IPv4 and IPv6). 
Singleprotocol router are only able to connect networks that use the same protocol.

# Router as Gateways
A router provides a gateway through which hosts on the local network can access the internet or other networks. 
In order for a host to access the gateway it must now the IP address of the router interface facing the local network, known as the *default gateway address*. This address can be obtained by either being statically assigned by a network administrator or automatically by using [[(DHCPv4) Dynamic Host Configuration Protocol]].
>[!note]
>As a router is the gateway to remote networks it also functions as a boundary between networks
# Routing
At each hop along the path, a router performs the following Layer 2 functions:
1. Accepts a frame from a medium
2. De-encapsulate the frame
3. Rr-encapsulate the packet into a new frame
4. Forward the new frame to the next hop

[[Routing]]
# Router Configuration
#Cisco_CLI 
We use the [[Cisco IOS CLI]] to configure the router.
## Basic Steps

>[!tip]
>With the command `no ip domain-lookup` you can disable DNS lookup to prevent the router from attempting to translate incorrect commands as host names.
>
>`R1(config-line)# logging synchronous` prevents notifications to interrupt your input


1. Configure device name
   `Router(config)# hostname Router1`

2. Secure privileged EXEC mode.
   Optional: `Router(config)# security passwords min-length lengthNumber`
   `Router(config)# enable secret password`

- (Set Domain Name)
  `Router(config)# ip domain-name domainName`

3. Secure user EXEC mode.
   `Router(config)# line console 0`    
   `Router(config-line)# password password`    
   `Router(config-line)# login`

4. [[Cisco IOS CLI#Configure SSH|Configure SSH]]

5. Secure remote Telnet / SSH access.
   `Router(config-line)# line vty 0 4`
   `Router(config-line)# password password`
   `Router(config)# login block-for 120 attempts 3 within 60`
   `Router(config-line)# login`
   `Router(config-line)# transport input {ssh | telnet}`

6. Secure all passwords in the config file.
   `Router(config)# service password-encryption`

7. Provide legal notification.
   `Router(config)# banner motd delimiter message delimiter`

8. Save the configuration.
   `Router(config)# end`
   `Router# copy running-config startup-config`

### Example
1. Configure device name
```
Router> enable
Router# configure terminal
Router(config)# hostname R1
```
2. Secure privileged EXEC mode.
```
R1(config)# enable secret class
```
3. Secure user EXEC mode.
```
R1(config)# line console 0
R1(config-line)# password cisco
R1(config-line)# login
```
4. Secure remote Telnet / SSH access.
```
R1(config)# line vty 0 4
R1(config-line)# password cisco
# block login for 120 seconds after 3 attempts within 60 seconds
Router(config)# login block-for 120 attempts 3 within 60
R1(config-line)# login
R1(config-line)# transport input ssh telnet
```
5. Secure all passwords in the config file.
```
R1(config)# service password-encryption
```
6. Provide legal notification.
```
R1(config)# banner motd # WARNING: Unauthorized access is prohibited! #
```
7. Save the configuration.
```
R1# copy running-config startup-config
```
## Configure Interfaces
- `Router(config)# interface type-and-number`
- `Router(config-if)# description description-text`
- `Router(config-if)# ip address ipv4-address subnet-mask`
- `Router(config-if)# ipv6 address ipv6-address/prefix-length`
- `Router(config-if)# ipv6 address ipv6-address link-local`
- `Router(config-if)# speed {DataRate | auto}`
- `Router(config-if)# duplex {half | full | auto}`
- `Router(config-if)# no shutdown`

**Example**
```
R1(config)# interface gigabitEthernet 0/0/0
R1(config-if)# description Link to LAN
R1(config-if)# ip address 192.168.10.1 255.255.255.0
R1(config-if)# ipv6 address 2001:db8:acad:10::1/64
R1(config-if)# speed auto
R1(config-if)# duplex auto
R1(config-if)# no shutdown
R1(config-if)# exit
```
### Speed
- maximum rate at which the interface can send and receive traffic in bits per second
- *FastEthernet*: supports 10 and 100 Mbps
- *GigabitEthernet*: supports 10, 100 and 1000 Mbps
- *autonegotiation* automatically determines the matching speed between two devices and is enabled by default

>[!tip]
>If the neighboring device does not use autonegotiation, you should manually configure the speed setting

**Example**
```
R1(config)# interface g0/1
R1(config-if)# speed ?
 10 Force 10 Mbps operation 
 100 Force 100 Mbps operation 
 1000 Force 1000 Mbps operation 
 auto Enable AUTO speed configuration 
R1(config-if)# speed 1000
```
### Duplex
The *duplex* setting refers to whether it is able to send and receive data at the same time or not:
- *Half duplex*: The interface cannot send and receive data at the same time
- *Full duplex*: The interface can send and receive data at the same time

**Example**
```
R1# configure terminal
R1(config)# interface g0/1 
R1(config-if)# duplex full 
R1(config-if)# interface range f0/1-2 
R1(config-if)# duplex auto
```
### Loopback Interfaces
The Loopback Interface is a logical interface, used in testing and managing Cisco IOS devices. It is automatically placed in an "up" state, as long as the router is functioning and it is not assigned to a physical port.
To configure a loopback interface:
```
Router(config)# interface loopback number
Router(config-if)# ip address ip-address subnet-mask
```
**Example:**
```
R1(config)# interface loopback 0
R1(config-if)# ip address 10.0.0.1 255.255.255.0
R1(config-if)# exit
R1(config)#
%LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback0, changed state to up
```
### Configure default Gateway
To configure the default gateway of a device use:
```
R1(config)# interface interfaceName
R1(config-if)# ip default-gateway ip
```
### Verification
#### Verify Interface Status
You can verify that the interfaces are active and operational with the commands:
- `R1# show ip interface brief`
- `R1# show ipv6 interface brief`
**Example**
```
R1# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0/0   192.168.10.1    YES manual up                    up
GigabitEthernet0/0/1   192.168.11.1    YES manual up                    up
Serial0/1/0            209.165.200.225 YES manual up                    up
Serial0/1/1            unassigned      YES unset  administratively down down
R1# show ipv6 interface brief
GigabitEthernet0/0/0   [up/up]
    FE80::7279:B3FF:FE92:3130
    2001:DB8:ACAD:1::1
GigabitEthernet0/0/1   [up/up]
    FE80::7279:B3FF:FE92:3131
    2001:DB8:ACAD:2::1
Serial0/1/0            [up/up]
    FE80::7279:B3FF:FE92:3130
    2001:DB8:ACAD:3::1
Serial0/1/1            [down/down]     Unassigned
```
#### Verify IPv6 Link Local and Multicast Addresses
You can verify the IPv6 addresses with 
- `R1# show ipv6 interfaces brief`
- `R1# show ipv6 interface interfaceID`
#### Verify Interface Configuration
You can display the current commands applied to a interface with 
- `R1# show running-config interface`

**Example**
```
R1 show running-config interface gigabitethernet 0/0/0
Building configuration...
Current configuration : 158 bytes
!
interface GigabitEthernet0/0/0
    description Link to LAN 1
    ip address 192.168.10.1 255.255.255.0
    negotiation auto
    ipv6 address 2001:DB8:ACAD:1::1/64
end
R1#
```
#### Verify Routes
Displays the entries in the routing table:
- `R1# show ip route`
- `R1# show ipv6 route`

```
R1# show ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
      
Gateway of last resort is not set
      192.168.10.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.10.0/24 is directly connected, GigabitEthernet0/0/0
L        192.168.10.1/32 is directly connected, GigabitEthernet0/0/0
      192.168.11.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.11.0/24 is directly connected, GigabitEthernet0/0/1
L        192.168.11.1/32 is directly connected, GigabitEthernet0/0/1
      209.165.200.0/24 is variably subnetted, 2 subnets, 2 masks
C        209.165.200.224/30 is directly connected, Serial0/1/0
L        209.165.200.225/32 is directly connected, Serial0/1/0
```
>[!info]
>The letters next to a route indicates:
>- **C**: directly connected route
>- **D**: EIGRP learned route
>- **L**: local route
>- **R**: RIR learned route

## IPv6 Configuration

### Enable IPv6 Routing
```
R1(config)# ipv6 unicast-routing
```
### GUA
```
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ipv6 address 2001:db8:acad:2::1/64
R1(config-if)# no shutdown
R1(config-if)# exit
R1(config)# interface serial 0/1/0
R1(config-if)# ipv6 address 2001:db8:acad:3::1/64
R1(config-if)# no shutdown
```
### LLA
```
R1(config)# interface gigabitethernet 0/0/0
R1(config-if)# ipv6 address fe80::1:1 link-local
R1(config-if)# exit
R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ipv6 address fe80::2:1 link-local
R1(config-if)# exit
R1(config)# interface serial 0/1/0
R1(config-if)# ipv6 address fe80::3:1 link-local
R1(config-if)# exit
```
## AutoSecure
```
Router# **auto secure**

                --- AutoSecure Configuration ---

*** AutoSecure configuration enhances the security of

the router but it will not make router absolutely secure

from all security attacks ***
```
## Additional Password Security
```
R1(config)# **service password-encryption**

R1(config)# **security passwords min-length 8**

R1(config)# **login block-for 120 attempts 3 within 60**

R1(config)# **line vty 0 4**

R1(config-line)# **password cisco123**

R1(config-line)# **exec-timeout 5 30**

R1(config-line)# **transport input ssh**

R1(config-line)# **end**

R1#

R1# **show running-config | section line vty**

line vty 0 4

password 7 094F471A1A0A

exec-timeout 5 30

login

transport input ssh

R1#
```
## Configure SSH
```
Router# **configure terminal**

Router(config)# **hostname R1**

R1(config)# **ip domain name span.com**

R1(config)# **crypto key generate rsa general-keys modulus 1024**

R1(config)#

R1(config)# **username Bob secret cisco**

R1(config)# **line vty 0 4**

R1(config-line)# **login local**

R1(config-line)# **transport input ssh**

R1(config-line)# **exit**

R1(config)#
```
