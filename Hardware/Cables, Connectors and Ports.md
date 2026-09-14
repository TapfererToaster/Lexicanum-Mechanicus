#CCNA
# Copper Twisted-Pair Cables

>[!note]
>TP cables are often called "Ethernet cables", but be aware that [[Ethernet]] is a standard that makes use of both TP and fibre-optic cables

## Anatomy
 Twisted-Pair Cables consist of up to 4  pairs of wires that are twisted around each other. 
 Die Verdrillung der Kabelpaare hebt das induzierte Magnetfeld der Leiter auf, wodurch Übersprechen auf die anderen Adern und die Wirkung von elektomagnetischer Störung reduziert wird. 

>[!note]
>Die einzelnen Aderpaare müssen unterschiedlich stark verdrillt werden.

Die einzelnen Leiter können dabei in zwei Formen vorliegen:
- *Litze*: Die Leiter bestehen aus mehreren Einzeldrähten, sind flexibler aber haben eine höhere Signaldämpfung.
  -> für kurze Verbindungen (z.B. Computer zu Wanddose) oder als Patchkabel
- *Massivleiter*: Der Leiter besteht aus einem massiven Leiter, dürfen nicht geknickt oder stark gebogen werden aber haben eine geringere Signaldämpfung.
  -> für dauerhafte Installationen (z.B. Verteiler zu Anschlussdosen) oder im [[Network Concepts & Basics#Backbone|Backbone-Netz]] 

## Categories
TP Kabel sind in verschieden Kategorien eingeteilt, die Eigenschaften der Kabel angeben.

>[!note]
>Die Standards werden von der [[Organizations#Electronic Industries Alliance (EIA)|EIA]]/[[Organizations#Telecommunications Industry Association (TIA)|TIA]] und der [[Organizations|ISO]] formuliert und von der [[Organizations#Deutsche Institut für Normung|DIN]] abgeleitet. 
>Zusätzlich gibt es die Europanormen DIN EN 50173 und EN 50174.
## Connectors
**8P8C / RJ-45**
Twisted-Pair cables usually use a *8 position 8 contact (8P8C)* connector, often referred to as a *Registered Jack-45 (RJ45)* connector.

**Augmented RJ-45 (ARJ-45)**
Identisch zu RJ-45 Stecker und Buchse, jedoch mit verbessertem Dämpfungsverhalten und somit größerem übertragbaren Frequenzbereich bis 5 GHz.

**GigaGate 45 (GG 45)**
Von der Firma Nexans entwickelte Stecker, welche gegenüberliegende Kontakte und eine innere Schirmung haben, durch die die Bandbreite erhöht und Nebensprechen reduziert ist.
## Schirmarten
Twisted-Pair cables can have different buildups, which protect them from interference:
- *Unshielded (U)*:
  Inside the cable are only the wire pairs and no further components
  -> no protection against *electromagnetic interference (EMI)* 
- *Shielded (S)*:
  A metallic shield, is either wrapped around all wires or the individual wire pairs
  -> protected against EMI
-  *Foiled (F)*:
  A metallic foil is either wrapped around all wires (F/xTP) or every wire pair individually (FTP)
  -> protected against EMI
  
  >[!note] Cabling Terminology
  >To describe the type of cable the form *XX/YZZ* is used:
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
Rollover cables are used to connect a PC to the console port of legacy network devices.
![[Rollover Cable.png]]
# Fiber-optic connections

>[!note]
>Die schon in den 1980er Jahren verlegten Glasfaserkabel für Kabelfernsehen, besaßen in der ursprünglichen Version keine Rückkanalfähigkeit, es konnten also nur Daten empfangen nicht aber gesendet werden.
## Anatomy
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

## Connectors
Fiber-optic connections have two cables, one for transmission and one for receiving. These are connected to a *Small Form-Factor Pluggable (SFP)*, which is plugged into a SFP port on a device.
>[!note]
>When connecting two devices, the SFP transceivers have to be plugged the correct way. The transmitter must be connected to the others receiver and vice versa. 

**Mechanical Transfer Registered Jack (MTRJ)**
Duplex Stecker, löste den SC-Duplex Stecker ab

**Straight Tip (ST)**
Stecker mit Bajonettverschluss

**Subscriber Connector (SC)**
Normstecker für Glasfaserverbindungen zum Endgerät

**LSA (DIN Stecker 47256)**

**Fiber connector (FC)**

**Lucent Connector (LC)**
Löste den MTRJ Stecker ab

**E2000**

## Tranceiver
Zur Umwandlung von elektrisch <-> optischen Signalen werden Tranceiver eingesetzt.
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

# Übertragungseigenschaften
**Signaldämpfung / Insertion Loss (IL)**
Gibt an wie stark sich Signale über eine Strecke abschwächen.

**Übersprechdämpfung / Near End Cross Talk (NEXT)**
Gibt an wie gut die einzelnen Adern in TP Kabeln gegen wechselseitige Beeinflussung (*Übersprechen*) geschützt sind. Dies wird durch die Verdrillung der Adern bewirkt.

**Attenuation To Crosstalk Ratio (ACR)**
Gibt das Dämpfungsverhalten als Different aus Signaldämpfung und Übersprechdämpfung an, ein höherer Wert bedeutet ein besseres Dämpfungsverhalten.

**Störempfindlichkeit**
Gibt an wie gut das Kabel gegen elektromagnetische Störeinflüsse geschirmt ist.

# Verkabelung
## Strukturierte Verkabelung
### Standards
Internationale Standards für die Verkabelung sind unteranderem ISO/IEC DIS 11801 und in Deutschland DIN EN 50173.

In den Standards werden Topologien und Kenndaten der Übertragungen definiert, sowie Link-Klassen zu denen Ende-zu-Ende-Verbindungen

**EN 50173**
In diesem Standard wird die Verkabelungsstruktur in drei Bereich geteilt und soll eine Planungssicherheit für mehrere Jahre sicher stellen.

*Primärverkabelung*: zwischen Gebäuden
[[Network Concepts & Basics#Backbone|Backbone Netz]] das Verbindungen zwischen Gebäude- und Standortverteiler per Glasfaser verbindet und diese an ein [[Network Concepts & Basics#Wide Area Network (WAN)|WAN]] anbindet.

*Sekundärverkabelung*: zwischen Etagen
Die Sekundärverkabelung verbindet den Gebäudeverteiler mit den Etagenverteilern, am besten mit Glasfaser.

*Tertiärverkabelung*: auf der Etage
Die Tertiärverkabelung verbindet die einzelnen Endgeräte mit den Etagenverteilern. 

## Collapsed Backbone
Bei der Verkabelung zu einem collapsed backbone werden alle Netzsegmente in einem Gerät gebündelt, das somit zum Backbone wird.

## Distributed Backbone
Hier erfolgt eine Dezentralisierung des Backbones, indem mehrere Geräte zur Zusammenfassung der Verbindungen verfügbar sind und die Kommunikation der angeschlossenen Geräte koordinieren.