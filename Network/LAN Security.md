#CCNA 
# Endpoint Security Devices
![[Endpoint Security.png|583x373]]

Attacks on LAN network devices can originate from outside but also from inside the network.
Endpoint devices inside LANs consist commonly of laptops, desktops, servers and employee owned phones through a *Bring your own device (BYOD)* policy.   
These are susceptible to malware attacks originating from email or web browsing and downloading files.  
Besides traditional host-based security, such as antivirus, firewalls and host-based intrusion prevention systems (HIPSs), a combination of Network access control (NAC), host-based Advanced Malware Protection (AMP), email security appliance (ESA) and web security appliance (WSA) are used.
- **VPN-enabled Router**: 
  provides a secure connection over a public network
- **Next-generation Firewall (NGFW)**: 
  provides stateful packet inspection, application visibility and control, *next generation intrusion prevention system (NGIPS)*, *advanced malware protection (AMP)* and URL filtering
- **Network Access Control (NAC)**: 
  devices include authentication, authorization and accounting (AAA) services
- **Email Security Appliance (ESA)**:  
  monitors [[Email#(SMTP) Simple Mail Transfer Protocol|Simple Mail Transfer Protocol (SMTP)]] traffic
	- Block unknown threats
	- Remediate against stealth malware that evaded initial detection
	- Discard emails with bad links
	- Block access to newly infected sites
	- Encrypt content in outgoing email to prevent data loss
- **Web Security Appliance (WSA)**: 
  Complete control of how users or applications access the internet
	- URL blacklisting
	- URL filtering
	- malware scanning
	- URL categorization
	- Web application filtering
	- de-/encrypting web traffic
# Access Control
## Authentication
*Authentication*: Who you are
### Local Authentication
Local authentication stores usernames and passwords in a local database on a network device, such as a router. 
### Server-Based Authentication
The usernames and passwords are stored on a AAA server and the router uses *Remote Authentication Dial-in User Service (RADIUS)* or *Terminal Access Controller Access Control System (TACACS+)* to communicate with the server and authenticate the entered username and passwords.

## Authorization
*Authorization*: What you can do

## Accounting
*Accounting*: What you did

# IEEE 802.1X
This standard is a port-based access control and authentication protocol that denies unauthorized workstations from connecting to a LAN through a publicly accessible switch port. Before the client has access to the LAN a authentication server must first authenticate the client.
![[IEEE 802.1X.png]]
- *Supplicant* (Client): a device running IEEE 802.1X-compliant client software
- *Authenticator* (Switch): requests identifying information from the client, relays that information to the authentication server and sends it's response back to the client; a wireless accesspoint can also act as an Authenticator
- *Authentication Server*: validates the identity of the client and notifies the Authenticator to grant or deny LAN access to the client

# Layer 2 / Switch Vulnerabilities
>[!important]
>- Always use secure variants of these protocols such as SSH, Secure Copy Protocol (SCP), Secure FTP (SFTP), and Secure Socket Layer/Transport Layer Security (SSL/TLS).
>- Consider using out-of-band management network to manage devices.
>- Use a dedicated management VLAN where nothing but management traffic resides.
>- Use ACLs to filter unwanted access.
## Switch Attacks
- *MAC Table Attacks*: MAC address flooding
- *VLAN Attacks*: VLAN hopping, VLAN double-tagging
- *DHCP Attacks*: DHCP starvation, DHCP spoofing
- *ARP Attacks*: ARP spoofing, ARP poisoning
- *Address Spoofing*: MAC and IP address spoofing
- *STP Attacks*: STP manipulation

**Switch Attack Mitigation**
- *Port Security*: prevents MAC address flooding, DHCP starvation
- *DHCP Snooping*: prevents DHCP spoofing, DHCP starvation
- *Dynamic ARP Inspection (DAI)*: prevents ARP spoofing, ARP poisoning
- *IP Source Guard (IPSG)*: prevents MAC and IP address spoofing

## MAC Address Table Attacks
MAC tables have a fixed size resulting that a switch can run out of space to store MAC addresses. This can lead to MAC address flooding, meaning that the switch will broadcast every fram it receives.
- **MAC flooding**: use a tool like [macof](https://www.kali.org/tools/dsniff/#macof) to generate fake MAC addresses and flood the switch until the MAC table "overflows", all traffic will be broadcasted allowing an attacker to capture all frames sent on the LAN/VLAN

**Mitigation**
To mitigate MAC flooding Portsecurity must be implemented.

## Port Security

#### Secure Unused Ports
It is best practice to disable all unused switch ports, by either navigating to each individual unused port or by defining a range of ports: `Switch(configif-range)# shutdown`

```
Switch(config)# interface range fa0/8 - 24
Switch(configif-range)# shutdown
```
>[!note]
>If the switch ports are needed simply activate them with the `no shutdown` command.

#### Enable Port Security
Port security limits the number of valid MAC addresses allowed on a port.
To enable port security use: `Switch(config-if)# switchport port-security` 

>[!important]
>The `switchport port-security` command can only be used on manually configured [[(VLAN) Virtual LAN#Access Port Assignment|access]] or [[(VLAN) Virtual LAN#Trunk Configuration|trunk]] port. 

```
Switch(config)# interface f0/1
# if not already configured
Switch(config-if)# switchport mode access/trunk
Switch(config-if)# switchport port-security
```

>[!warning]
>If the switch detects multiple unique MAC addresses on the port, the port transitions to an `error-disabled` state and blocks traffic on it. Further all dynamically learned addresses will be forgotten. 

Use `show port-security interface` to display the current security settings of a port.
```
Switch# show port-security interface f0/1
```
#### Limit MAC Addresses
Set a maximum number of MAC addresses allowed on a port use:
`Switch(config-if)# switchport port-security maximum addressNumber`

```
S1(config)# interface f0/1
S1(config-if)# switchport port-security maximum 50
```
#### Learn MAC Addresses
On a secure port the switch can learn MAC addresses in three ways:
- **Manually Configure**
  The administrator manually configures a static MAC address with the following command for each address
  `Switch(config-if)# switchport port-security mac-address macAddress (vlan vlanName)`
```
  Switch(config-if)# switchport port-security mac-address aa:bb:cc:11:22:33 (vlan HQ)
```
- **Dynamically Learned**
  When the `switchport port-security`command is entered, the current source MAC for the device connected to the port is automatically secured, but it is not added to the startup configuration. 
  If the switch is rebooted, the port will have to re-learn the device's MAC address.
- **Dynamically Learned Sticky**
  With this command the switch learns the MAC address dynamically and adds it to the running configuration. 
  When saving the running config the MAC address is saved to NVRAM.
  ```
  Switch(config-if)# switchport port-security mac-address sticky
  ```

>[!note]
>A MAC address learned on a `port-security` enabled port is called a *secure MAC address*.

#### Port Security violation modes
Security *violation modes* are used to configure the behavior of a `port-security` enabled port when a security violation occurs.
These modes are:
- **shutdown**
  the port is shut down and all communication is stopped; default
- **restrict**
  frames that violate the MAC address limit are discarded, but communication with already known MAC is continued, the violation counter is incremented with each violating frame, generates a Syslog message and SNMP Traps/Informs
- **protect**
  frames that violate the MAC address limit are discarded, communication is continued and the violation counter is not incremented


| Mode     | Discards Offending Traffic | Sends Syslog Message | Increases Violation Counter | Shuts Down Port |
| -------- | -------------------------- | -------------------- | --------------------------- | --------------- |
| Protect  | Yes                        | No                   | No                          | No              |
| Restrict | Yes                        | Yes                  | Yes                         | Yes             |
| Shutdown | Yes                        | Yes                  | Yes                         | Yes             |


To configure a violation mode on a port use:
`S1(config-if)# switchport port-security violation {protect | restrict | shutdown}`

```
S1(config)# interface f0/1
S1(config-if)# switchport port-security violation restrict
```

**Error-disabled State**
When a violation in the `shutdown` mode occurs, the port is physically shutdown, is placed in the error-disabled state and no traffic is sent or received on it.
To activate the port enter the port interface then:
1. `S1(config-if)# shutdown`
2. `S1(config-if)# no shutdown`
#### MAC address aging
>[!note] Reminder
>MAC address aging refers to the time a MAC address is stored in the MAC address table before it is discarded. The timer resets whenever a frame from the corresponding address is received.

By default secure MAC addresses do not age and stay in the address table as long as the port it was learned on stays up.
To enable secure MAC address aging use 
`Switch(config-if)# switchport port-security aging { static | time minutesNumber | type absolute | inactivity}`

```
SW1(config)# interface f0/1
SW1(config-if)# switchport port-security aging time 5
SW1(config-if)# switchport port-security aging type inactivity
```

**Parameters**
- `static`: Enable aging for statically configured secure addresses 
- `time`: Set the aging time between 0 to 1440 minutes, if `0` is set aging is disabled
- `type absolute`: The addresses age out exactly after the set time and are removed; default 
- `type inactivity`: The addresses age out only if there is no data traffic for the specified time period

 **Static Secure MAC Address Aging**
Manually configured static MAC address do not age out and usually need to be manually removed. However this can be changed with:
```
SW1(config)# interface f0/1
SW1(config-if)# switchport port-security aging static
```

#### Verify Port Security
- **Port Security for all interfaces**:
  `S1# show port-security`
- **Port Security for a Specific Interface**:
  `S1# show port-security interface interfaceID`
  
```
  S1# show port-security interface fastethernet 0/1
```
- **Verify Learned MAC Addresses**
  `S1# show run interface interfaceID`
  
``` 
S1# show run interface fa0/1
```
- **Verify Secure MAC Addresses**
  `S1# show port-security address  `


## VLAN attacks
### VLAN Hopping
This attack enables the attacker to see traffic from other VLANs without a router, by configuring a host to spoof 802.1Q and [[(VLAN) Virtual LAN#Dynamic Trunking Protocol (DTP)|DTP]] signaling to trunk with a connected switch, if successful the attacker can access the VLANs on the switch and send and receive traffic from them.

### VLAN Double-Tagging
In this attack a 802.1Q tag is hidden inside a frame that already has an 802.1Q tag. This allows the frame to be sent to a VLAN that the original tag did not specify.
1. The attacker sends a frame to the switch which has a tag to the native VLAN and a inner tag for the victims VLAN
2. The switch receives the frame and inspects the first tag and forwards the frame out of all native VLAN ports after stripping the tag. 
3. When the frame is received on another switch it again checks the tag, which is addressed to the victims VLAN and forwards the frame to the victim or floods the VLAN.

### VLAN Attack Mitigation
- Disabling trunking on all access ports
- Disable auto trunking on trunk links so that trunks must be manually enabled
- Be sure that the native VLAN is only used for trunk links

### Mitigating VLAN Attacks
VLAN hopping can be accomplished  in three ways:
- Spoofing DTP messages from the attacking host to cause the switch to enter trunking mode. From here, the attacker can send traffic tagged with the target VLAN and the switch then delivers the packets to the destination.
- Introducing a rogue switch and enabling trunking. The attacker can then access all the VLANs on the victim switch from the rogue switch.
- Another type of VLAN hopping attack is a double-tagging attack. 

#### Steps to mitigate VLAN hopping
**Access Port**
1. Disable DTP (auto-trunking) negotiations on non-trunking ports:
   `S1(config-if-range)# switchport mode access` 
2. Disable unused ports and put them in an unused VLAN
   `S1(config-if-range)# switchport access vlan 1000
   `S1(config-if-range)# shutdown`

```
S1(config)# interface range fa0/17 - 20
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan 1000
S1(config-if-range)# shutdown
S1(config-if-range)# exit
```

**Trunk Port**
1. Manually enable the trunk link on a trunking port
    `switchport mode trunk` 
2. Disable DTP (auto-trunking) negotiations n trunking ports
    `switchport nonegotiate` 
3. Set the native VLAN to a VLAN other than VLAN 1
    `switchport trunk native vlan vlan-number`

```
S1(config)# interface range fa0/21 - 24
S1(config-if-range)# switchport mode trunk
S1(config-if-range)# switchport nonegotiate
S1(config-if-range)# switchport trunk native vlan 999
S1(config-if-range)# end
```

## DHCP Attacks
### DHCP Starvation
In this attack a attacker uses tools like [Gobbler](https://sourceforge.net/projects/gobbler/) to try to lease the entire IP pool with fake MAC addresses. This creates a DoS for connecting clients as they are unable to receive a IP address.
### DHCP Spoofing
This attack is done by connecting a rouge DHCP server to a network, which provides false IP configuration parameters to connecting clients:
- **default gateway**: the default gateway given to the host can be used for a man-in-the-middle attack
- **DNS server**: the rouge DNS server point the clients to malicious websites
- **IP**: provides a fake IP address creating a DoS attack on the client

### Mitigating DHCP Attacks
In a DHCP poisoning attack an attacker configures a rogue DHCP server that leases IP addresses so the clients uses it as their default gateway. 

#### DHCP Snooping 
DHCP snooping is a security feature on Cisco switches that examines and filters DHCP messages.
Steps:
1. Enable DHCP snooping:
    `SW1(config)# ip dhcp snooping`
2. Set trusted ports: 
   `S1(config-if)# ip dhcp snooping trust`
3. Limit the number of DHCP discovery messages on untrusted ports: 
   `ip dhcp snooping limit rate packetNumber`
4. Enable DHCP snooping by for VLANs
   `SW1(conifg)# ip dhcp snooping vlan vlanId`

```
S1(config)# ip dhcp snooping
S1(config)# interface f0/1
S1(config-if)# ip dhcp snooping trust

S1(config)# interface range f0/5 - 24
S1(config-if-range)# ip dhcp snooping limit rate 7
S1(config-if-range)# exit
S1(config)# ip dhcp snooping vlan 5,10,50-52
```

You can also activate DHCP Snooping on multiple VLANs, as it is advised to enable DHCP snooping in every VLAN that has hosts using DHCP.
```
SW1(conifg)# ip dhcp snooping vlan 4
SW1(config)# ip dhcp snooping vlan 1-10
SW1(config)# ip dhcp snooping vlan 1,2,3-5,6,7-10
```

**Trusted and untrusted ports**
Packets received on untrusted ports are filtered by DHCP snooping and all ports are untrusted by default. 
Frames received on trusted ports are allowed, but you have to manually configure each trusted port with:
```
SW1(conifg)# interface g0/1
SW1(config-if)# ip dhcp snooping trust
```

Ports that face towards the DHCP server should be trusted and DHCP snooping will forward DHCP messages on those ports without inspection.
Ports that face away from the server should be untrusted and will be inspected as follows:
- If it is a DHCP server (OFFER, ACK or NAK) message discard it
- If it is a DHCP client message (DISCOVER, REQUEST, DECLINE or RELEASE) inspect it further 
- If a client successfully leases an IP address, create a new entry in the DHCP Snooping binding table 
## ARP attacks
**Address Spoofing**
An attacker can spoofs the IP and MAC address of his computer by using an valid IP address or changing the MAC address of their computer to match the address of an target inside the network.

**ARP poisoning**
Clients can send an *gratuitous ARP* Request, which leads the other hosts on the network to store the MAC address and the IP address.
This can be used by an attacker to get a switch to store the ARP entry.

Tools to facilitate such attacks are:
- dsniff
- Cain&Abel
- ettercap
- Yersinia

### Dynamic ARP Inspection (DAI)
DAI requires DHCP snooping and ensures that only valid ARP Requests and Replies are relayed.
This is ensured by:
- Not relaying invalid or gratuitous ARP Requests out to other ports in the same VLAN
- Intercepting all ARP Requests and Replies on untrusted ports
- Verifying each intercepted packet for a valid IP-to-MAC binding
- Dropping and logging ARP Requests coming from invalid sources to prevent ARP poisoning
- Error-disabling the interface if the configured DAI number of ARP packets is exceeded

Steps:
1. Enable DHCP snooping
   `S1(config)# ip dhcp snooping`
2. Enable DHCP snooping on VLANs
   `S1(config)# ip dhcp snooping vlan vlanID`
3. Enable DAI on  VLANs
   `S1(config)# ip arp inspection vlan vlanID`
4. Configure trusted interfaces 
   `S1(config-if)# ip dhcp snooping trust`
   `S1(config-if)# ip arp inspection trust`

```
S1(config)# ip dhcp snooping
S1(config)# ip dhcp snooping vlan 10
S1(config)# ip arp inspection vlan 10
S1(config)# interface fa0/24
S1(config-if)# ip dhcp snooping trust
S1(config-if)# ip arp inspection trust
```

DAI can be configured to check the destination or source address:
- Check the source MAC address in the Ethernet header against the address in the ARP body.
  `S1(config)# ip arp inspection validate src-mac`
- Check the destination MAC
  `S1(config)# ip arp inspection validate dst-mac`
- Check the ARP body for suspicious IP addresses including `0.0.0.0`, `255.255.255.255` and multicast IP addresses.
  `S1(config)# ip arp inspection validate ip`
## STP Attack
Attackers can manipulate the STP to disrupt the network or make their system appear as a root bridge.
This is done by broadcasting  STP bridge protocol data units (BPDUs) containing configuration and topology changes with the goal that the attackers computer will become root bridge.

### Mitigating STP Attacks 
To mitigate STP attacks implement PortFast and *Bridge Protocol Data Unit (BPDU)* Guard
**PortFast**: immediately brings an interface configured as an access port to the forwarding state from a blocking state; should only be configured on ports attached to end devices
**BPDU Guard**: immediately puts a port that receives a BPDU into error-disable state; should only be configured on ports attached to end devices

**Configure PortFast**
- Enable PortFast on an interface:
  `S1(config-if)# spanning-tree portfast`
- Enable PortFast globally:
  `S1(config)# spanning-tree portfast default`

```
S1(config)# interface fa0/1
S1(config-if)# switchport mode access
S1(config-if)# spanning-tree portfast
```

**Configure BPDU Guard**
- Enable BPDU Guard on an interface:
  `S1(config-if)# spanning-tree bpduguard enable`
- Enable BPDU Guard globally:
  `spanning-tree portfast bpduguard default`

```
S1(config)# interface fa0/1
S1(config-if)# spanning-tree bpduguard enable
S1(config-if)# exit
S1(config)# spanning-tree portfast bpduguard default
```

If a port receives any BPDU it will be put into error-disabled state and must be re-enabled through `shutdown` and `no shutdown` or automatically recovered with `errdisable recovery cause bpduguard`
## Cisco Discovery Protocol (CDP)
This protocol is a Layer 2 link discovery protocol, which is used for auto-configuration of connections and troubleshoot networks.
The information sent can also be used by an attacker as the messages are broadcasted unencrypted and unauthenticated.

# Email Security
Phishing attacks are a form of email attack with the goal that an employee, gives away login credentials by opening a link or an attachment with malware.
Spear fishing targets high-profile employees or executives 
Phishing attacks make up the majority of attacks on enterprise networks.

Ciscos ESA monitors SMTP traffic and is constantly updated every three to five minutes by real-time feeds from Cisco Talos using worldwide data monitoring systems.
- **Email Security Appliance (ESA)**:  
  monitors [[Email#(SMTP) Simple Mail Transfer Protocol|Simple Mail Transfer Protocol (SMTP)]] traffic
	- Block unknown threats
	- Remediate against stealth malware that evaded initial detection
	- Discard emails with bad links
	- Block access to newly infected sites
	- Encrypt content in outgoing email to prevent data loss

# Web Security Appliance
WSA is a mitigation technology, securing and controlling web traffic. It combines advanced malware protection. application visibility and control.
It provides control over how users can access the internet, by blocking or allowing certain features and applications.
It also performs blacklisting of URLs, URL filtering, malware scanning, URL categorization, web application filtering and encrypting and decrypting traffic