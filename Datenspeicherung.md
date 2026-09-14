# Backup
Backups sind Sicherungen von Daten die aus dem System herausgenommen werden.
- Backups dürfen nicht durchgängig erreichbar sein 
- Ein eigener User account sollte für die Erstellung von Backups eingerichtet werden
- Backup Server sollten per Pull Prinzip die zu sichernden Daten selbstständig holen

# Redundant Array of Independent Disks (RAID)
RAID benutzt mehrere Festplatten um Redundanz  zu gewährleisten und/oder die Leistung zu erhöhen.

**RAID 0**: Stripe-Set
Daten werden auf parallel auf die Festplatten geschrieben
-> bessere Performance, keine Redundanz

**RAID 1**: Mirroring
Daten werden 1:1 auf ein zweites Laufwerk geschrieben
-> Performance bleibt gleich, Redundanz

**RAID 5**
Paritätsinformationen  werden auf alle Festplatten geschrieben
-> besser Performance, Redundanz (ein Laufwerk kann ausfallen)

**RAID 6**
Paritätsinformationen werden doppelt auf alle Festplatten verteilt
-> zwei Festplatten können Ausfalle

**RAID 10**
Kombination aus RAID 1 und RAID 0

**RAID 15**
Kombination aus RAID 1 und RAID 5

**Weitere**
RAID 50, 51, 60, 61, etc.

# Network Attached Storage (NAS)
Eine NAS ist ein Speicher der per Netzwerkanschluss an das Netzwerk eingebunden ist.
Sie bestehen aus einem Gehäuse und mehreren Steckplätzen für Festplatten.
Einige haben Hardware-RAID integriert.

# Storage Area Network (SAN)
Ein SAN ist ein Netzwerk, das  zum Speichern von Daten benutzt wird.

## Topologies
Most SAN environments within a fabric fall into three types:
**Collapsed Core**
In this topology servers and storage devices are connected to core switches.
There is single management per fabric.

**Core-Edge Topology**
In this topology servers connect to edge switches and storage devices connect to one or more core switches

**Edge-Core-Edge Topology**
In this topology servers and storage devices connect to edge switches which are connected to one or more core switches.

# Interfaces und Verbindungen
**Fibre Channel (FC)**
Fibre Channel nutzt das SCSI-3 Protokoll und kann mit einem FC Switch kombiniert werden.
Es kann eine Bandbreite von 16 Gb/s vollduplex erreicht werden.

**Fibre Channel Arbitrated Loop (FC-AL)** 
Erlaubt den Anschluss von 127 Geräten an einen logischen Bus.

**Fibre Channel Switch (FC-SW)**
Leistungsfähiger als FC-AL, werden mehrere FC-SW benutzt spricht man von einem Fibre Channel Fabric

**Fibre Channel over Ethernet (FCoE)**
Ist ein Protokoll das erlaubt Ethernet Verbindungen zu benutzten. Es hat weniger Overhead als iSCSI, da es direkt auf Ethernet basiert und nicht TCP oder IP Protokolle verwendet

**iSCSI**
iSCSI, SCSI über TCP/IP laut RFC 3720 ermöglicht es Ethernet Verbindungen zu benutzen

