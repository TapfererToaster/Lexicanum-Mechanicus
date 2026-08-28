# RA messages
The Bits for the messages are either `0` or `1`, each according to `true` or `false`
- **A flag**: Address Autoconfiguration Flag
	uses [[IPv6#Stateless Address Autoconfiguration (SLAAC)|Stateless Address Autoconfiguration (SLAAC)]]
	- the client creates its own IPv6 GUA using either *Extended Unique Identifier method (EUI-64)* or generate it randomly
- **O flag**: Other Configuration Flag 
  uses a stateless DHCPv6 Server
- **M flag**: Managed Address Configuration Flag
  uses a stateful DHCPv6 server


# RS Messages
A router will send RA messages if it receives RS messages from a client.
>[!note] 
>The client will send RA messages to the IPv6 routers multicast address `ff02::2`.

