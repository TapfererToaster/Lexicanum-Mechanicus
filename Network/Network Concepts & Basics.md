#CCNA 
# Network Models
A networking model is a framework that defines the necessary functions and components to enable communication via a network. The functions and components are usually separated into layers, with each of these describing a certain role, which are then fulfilled by one or more protocols. 

>[!note]
>A protocol is a set of rules that define how data is communicated between devices.

The two models that should be known are:
- [[(OSI) Open Systems Interconnection-Modell]]
- [[TCP-IP Modell]]

**Vendor-proprietary and vendor neutral**
In the past there have been many attempts to create models, many of those concepts were *vendor-proprietary*, meaning a single vendor created its own concept and protocols that were used by their products.
>[!note]
>An example for a vendor-proprietary network is [IBM's SNA](https://en.wikipedia.org/wiki/Systems_Network_Architecture).

In the end the *vendor neutral* approach was successful, with protocols that can be used by devices of all vendors (f.e. Linux, Windows and Mac computers can all use the same protocols and communicate with each other).

# Transmission 
Data is either transported via a *unbound media*, f.e radio waves, or *bound media*, f.e. [[Cables, Connectors and Ports|cables]].  
# Types

## Personal Area Network (PAN)
WPANs are based on the 802.15 standard and 2.4 GHz radio frequency.
Low powered transmitters for short range communication up to 10m and technologies like Bluetooth and ZigBee are used.
## Local Area Network (LAN)
>[!important] Defintion
>A group of interconnected devices in a limited area, such as an office.

![[LAN Topology.png]]

 A LAN is a network of connected devices in an area up to a few kilometers, with [[Switches]] being used to connect the devices inside a LAN and [[Router]] to connect LANs with each other and enable devices to communicate with remote networks, f.e. the internet.
 
>[!note]
>Another term for a LAN is a *[[(OSI) Open Systems Interconnection-Modell#2. Datensicherungsschicht (Data Link, Layer 2)|Layer 2 domain]]*, as the data is switched using the MAC address, without the Router.

**Wireless LAN (WLAN)**
In einem [[WLAN]] werden Daten nicht über Kabel, sondern über Funkwellen transpostiert. Zusätzlich werden Access Points und Home Router benutzt.

**Virtual LAN**
Bei einem [[(VLAN) Virtual LAN]] wird in dem LAN mehrere virtuelle Netzwerke erstellt, ohne weitere Hardware zu benötigen.

**Industrie LAN**
Industrie LANs sind LANs in industriellen Umfeld, wie Fertigungsanlagen.
Standards sind:
- Feldbus IEC 61158-1
- EtherNet Industrial Protocol (EIP)
- Process Field Bus (PROFIBUS)
- EtherCAT
- Process Field Network (PROFInet)

Die eingesetzten Geräte und Netzwerkkomponenten müssen dabei bestimmte Eigenschaften aufweisen:
- Gleichstrom-Spannungsversorgung (24 V DC)
- erweiterter Betriebstemperaturbereich
- Schutz gegen Staub, (Spritz-)Wasser, Schmutz, usw.
- Vibrationsfest
- erhöhte Verfügbarkeit von Komponenten

**PowerLAN / Powerline**
Ein PowerLAN überträgt Daten nicht über Ethernetkabel, sondern über das Stromnetz. Dazu werden Steckdosen Adapter benutzt.
## Metropolitan Area Network (MAN)
Umfasst eine Stadt, Gemeinde oder Region in einem Umkreis von 100 km und mehr.

## Wide Area Network (WAN)
Ein [[Wide Area Network (WAN)]] dient der Datenübertragung über große Distanzen die mehrere Städte, eine Region oder ein ganzes Land umfassen.
## Global Area Network (GAN)
Umfasst mehrere Länder, einen Kontinent oder die ganze Welt.
## Backbone
Ein *Backbone* Netz ist ein Hochleistungsnetz, das andere Teilnetze miteinander verbindet, so etwa die Netze von Gebäuden, Städten, usw.
# Topology
## Physical Topology
Die Topologie eines Netzwerkes beschreibt in welcher physikalischen Grundform die einzelnen Geräte organisiert und verbunden sind.
### Bustopologie
Bei einer Bustopologie werden die Geräte hintereinander an einen Kabelstrang angeschloßen. Die Enden des Kabelstrangs werden mit Abschlußwiderständen (Terminatoren) abgeschloßen. 
Die Geräte in einer Bustopologie führen keine Wiederaufbereitung des Signals durch, wodurch die Reichweite beschränkt ist, da die Signale schwächer werden. Um die Reichweite zu erhöhen müssen Repeater eingesetzt werden.

Signale werden in beide Richtungen des Kabels gesendet, wodurch es ein Diffusionsnetz ist.
### Sterntopologie
Bei einer Sterntopologie werden die Geräte an ein zentrales Gerät angeschloßen.  
### Ringtopologie
Bei einer Ringtopologie werden die Geräte an einem Kabelstrang ringförmig angeschloßen, wobei die Enden des Kabelstrangs nicht terminiert werden sondern einen geschloßenen Ring bilden.
Daten werden nur in einer Richtung gesendet, wodurch es zu keinen Kollisionen kommen kann, da die Dauer bis die Daten am Ziel ankommen berechnet werden kann.
Die Signale werden von den den einzelnen Geräten verarbeitet und weitergeleitet. 

Als Kabel werden Copper Distributed Data Interface (CDDI) Kupferkabel oder Fiber Distributed Data Interface (FDDI) Glasfaserkabel benutzt.
### Baumtopologie
Bei einer Baumtopologie gehen von einem Gerät aus mehrere Verästelungen ab, an denen sich weitere Geräte oder Netze befinden.

## Logical Topology
Die logische Topologie beschreibt wie die Geräte im Netzwerk logisch angeordnet sind, z.B. VLANs, Subnetze.

# Planung und Implementierung
## Planung
Bei der Planung eines Netzwerkes sollten einige Aspekte berücksichtigt werden:
- Welche Kabelwege existieren und wie können Kabel verlegt werden?
- Welches Übertragungsmedium soll eingesetzt werden?
- Wie werden die Daten übertragen und welche Zusammenhänge entstehen dadurch
- Welche Betriebssysteme werden benutzt 

# Shared and Switched Networks
- **Shared Networks**: all devices inside the network share the same media, resulting in the need for Access control methods, such as CSMA/CD and CSMA/CA
  f.e. legacy hub networks, WLAN
- **Switched Networks**: all devices inside the network have their own connection with the network 

# Netzwerküberwachung und -management
**Netzwerküberwachung**
Statusmeldungen und Betriebswerte der Netzwerkkomponenten werden zentral gespeichert. Bei Über- oder Unterschreitung von gesetzten Werten kann eine Aktion, z.B. eine Warnung oder ein Alarm, ausgeführt werden.

**Netzwerkmanagement**
Neben der Überwachung der Netzwerkkomponenten, können diese zentral konfiguriert und gesteuert werden.

**Systemmanagement**
Hier werden nicht nur die Netzwerkkomponente überwacht, sondern auch deren Bestandteile, wie Lüfter, Netzteil, Festplatten, usw.

Zur Netzwerküberwachung können Protokolle wie [[(SNMP) Network Management Protocol]] oder Sniffer wie [[Wireshark]] eingesetzt werden.

# -net Types
**Internet**
Das [[Internet]] ist das größte WAN/GAN, das weltweit Geräte miteinander verbindet.

**Intranet**
Intranet ist die Bezeichnung für ein lokales Netz, das Internetprotokolle, IPv4 und IPv6, verwendet um Geräte miteinander zu verbinden und z.B. Server bereitzustellen. 

**Extranet**
Laut ISO/IEC 2382 ist eine Extranet eine Erweiterung eines firmeneigenen Intranets das Zugriffe für externe Benutzer ermöglicht.

# Tunneling
Beim *Tunneling* werden Daten eines Protokolls in der payload eines anderen Protokolls transportiert. Am Ziel wird der Transportrahmen entfernt und die ursprünglichen Daten können verarbeitet werden.
Dies kann benutzt werden damit z.B. IPv6 Pakete über ein IPv4 Netzwerk oder Daten in einem VPN verschlüsselt über ein öffentliches Netz transportiert werden können.

Tunnelingprotokolle:
- Layer 2 Tunneling Protocol (L2TP)
- Internet Protocol Security (IPsec)
- OpenVPN

# Privatsphäre
## Nutzerdaten im Internet
Sobald eine Verbindung mit einem anderen Rechner oder Server besteht, ist diesem vom ISP [[Organizations#Regional Internet Registries (RIR)|vergebene]] IP-Adresse des Senders bekannt, welche Rückschlüsse auf den ungefähren Standorts des Nutzers ermöglicht. Speichert der ISP die IP Adressen kann man zusätzlich den angemeldeten Nutzernamen herausfinden.
Metadaten wie Verbindungsdaten oder Betreffzeilen werden auch oft unverschlüsselt übertragen. selbst bei verschlüsselten Mails oder dem Verbindungsaufbau per HTTPS.

>[!note]
>Man kann grundsätzlich davon ausgehen, dass alle Datenübertragungen und Tätigkeiten im Internet abgehört werden, Schutz dagegen ist nur eine starke Verschlüsselung.

## Anonymisierungs-Netzwerke
Anonymisierungs-Netzwerke, wie Tor, bieten Schutz durch Proxys, genauer zufällig verbundenen Rechnern aus einem registrierten Pool. 
Der Ziel-Server erfährt so nicht die IP Adresse des Clients und die Daten werden verschlüsselt im Netz übertragen, dies führt jedoch zu einer geringen Übertragungsrate.

## Nutzerprofile
Die Datensammlung von Nutzern ist möglich durch:
- Cookies
- Supercookies (Local Shared Objects, Flash Cookies)
- Tracking
- Browser-Fingerprints 
- Clock-Skew Fingerprints
- installierte Apps

Diese können einen Nutzer bzw. ein Gerät auch bei Benutzung eines Anonymisierungs-Netzwerkes identifizieren.

