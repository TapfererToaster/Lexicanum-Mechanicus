SNMP wird benutzt um Netzwerke und deren Komponente zu managen, genauer der Überwachung von Netzwerkkomponenten, der Gerätekonfiguration, Fehlererkennung und Alarmauslösung, sowie der Inventarisierung von Geräten.

Im Netzwerk wird eine Gerät als *Network Management Station (NMS)* konfiguriert und der Serverdienst SNMP-Manager wird implementiert.
Auf den Clients, *Managed Nodes*, werden SNMP-Agents installiert.
In einer *Management Information Base (MIB)* werden Informationen über die Clients gespeichert, auf die der SNMP-Manger Zugriff hat.

- *Polling*:
  Bezeichnet die periodische Abfrage der Managed Nodes von der NMS
- *Trap*: 
  Eine Mitteilung an den NMS die durch ein bestimmtes Ereignis ausgelöst wird.

**Operationen**
Der Server hat folgende Operationen die er ausführen kann:
- `get`: Abrufen von Daten aus der MIB
- `getnext`: Abruf des nächsten Datensatzes
- `getbulk`: Abrufen eines Datenblocks
- `walk`: Abrufen alle verfügbaren Datensätze in der MIB

Client:
- `response`: Antwort auf eine Operation
- `trap`: Senden einer Warnung oder eines Alarms 

MIB:
- `set` Setzen einer Variable 

**MIB**
In der Management Information Base werden die überwachenden Daten der Netzwerkkomponenten als Objekte mit Attributen gespeichert.
Objekte sind unter anderem Systeminformationen, Routing-Tabellen, Interfaces usw.
Die Struktur der Datenbank ist dabei von der *Structure of Management Information (SMI)* festgelegt.
Einzelne Objekte werden werden in einer hierarchischen Baum Topologie dargestellt. Dabei werden vom Wurzel Objekt die Standard-MIB und Private MIB abgeleitet.
Die Standard MIB beinhaltet Variablen die standardmäßig benutzt werden, wie System-, IP-, TCP- und Interface-Variablen.
Private MIB werden von Herstellern benutzt um herstellerspezifische oder proprietäre Werte abzubilden.

Versionen:
- MIB (RFC 1156)
- MIB 2 (RFC 1213)
- RFC 3418

# SNMPv2
Weiterentwicklung die Sicherheitsmechanismen und eine erweiterte Ressourcenverwaltung hinzufügt. 
SNMPv2 ist abwärtskompatibel und kann bestehende MIBs nutzen. 

Versionen
- RFC 1901-1907, 2578-2580
- SNMPv2p (Party-Based)
- SNMPv2u (User-Based)
- SNMPv2c (Community-Based)

# SNMPv3

# Remote Monitoring (RMON)
Eine Erweiterung von SNMP die es ermöglicht statistische Daten in Netzwerkkomponenten aufzuzeichnen und in einer Datenbank zu speichern. 

# SNMP-Manager

Zu unterscheiden sind zwischen SNMP-Applikationen, die primär Standard-MIBs auswerten, und proprietäre Programme von Herstellern.

Eine Open-Source Manager ist [Icinga](https://icinga.com/)

Die Funktionen von SNMP-Managern sind:
- Device-Management: Überwachung, Konfiguration und Troubleshooting von Geräten
- Topologie-Management: Visualisierung der Netzwerkstruktur
- Event-Management: Einstellen von Parametern 
- Accounting-Management: Protokollierung der Nutzung