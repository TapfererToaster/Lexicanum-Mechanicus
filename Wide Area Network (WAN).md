
**Bestandteile**
Benutzer sind über *Datenendeeinrichtung (DEE)*, z.B. DSL Modem, mit einer *Datenübertragungseinrichtung (DÜE)* verbunden, welche die Kommunikation über *Übertragungswege* mit anderen Geräten ermöglicht.

**Bandbreite**
Schmalband: Verbindungen mit Datendurchsatzraten von < 2Mbit/s
Breitband: Verbindungen mit Datendurchsatzraten von >= 2Mbit/s
# Arten 
- Public Switched Telephone Network (PSTN)
- Integrated Digital Network (IDN)
- Kabelfernsehnetz für Video- und Rundfunksendungen
- Unterseekabel 

# Verbindungsarten

## Festverbindungen
Festverbindungen sind fest geschaltete Verbindungen zwischen zwei Standorten, die permanent verfügbar sind und ohne Einwählvorgang genutzt werden können.

## Virtuelle Verbindung 
Bei virtuellen Verbindungen oder auch *Virtual Circuit* genannt, werden keine exklusiven festen Leitungen benutzt, sondern logische Verbindungen.

**Permanent Virtual Circuit (PVC)**
Bei einem PVC werden Daten schneller übertragen, da die Verbindungsweg von Beginn der Übertragung an bekannt ist

**Switched Virtual Circuit (SVC)**
Bei einer SVC muss am Beginn der Übertragung eine Verbindung aufgebaut und am Ende abgebaut werden.
Protokolle wie X.25 dun Synchronous Transfer Mode (ATM) kommen hier zum Einsatz.

## Corporate Network (IC)
Ein Corporate Network ist ein Zusammenschluss von mehreren LANs eines Unternehmens zu einem Netzwerk.
Zwischen den Standorten bestehen exklusive physische oder logische Verbindungen, die durch Netzinfrastruktur eines Provider oder Carrier realisiert werden können.

## Virtual Private Network (VPN)
Bei einem VPN bestehen logische Verbindungen zwischen einzelnen LANs, wobei die Kommunikation mit Hilfe von [[Network Concepts & Basics#Tunneling|Tunnelingprotokollen]] erfolgt.

## Remote Access Service (RAS)
RAS ist Dienst der es ermöglicht auf ein Firmennetz zuzugreifen.

# Vermittlung
**Paketvermittlung**
![[Paketvermittlung.png]]
Bei der Paketvermittlung werden Pakete nicht über eine dedizierte physische Verbindung zwischen Sender und Empfänger gesendet, sondern über mehrere Stationen, z.B. Router und mehrere mögliche Wege.

**Leitungsvermittlung**
![[Leitungsvermittlung.png]]
Hier besteht eine dauerhafte physische oder virtuelle Verbindung zwischen Sender und Empfänger. Zur Übertragung von Daten wird eine feste Verbindung aufgebaut und am Ende abgebaut.
# Datenfernübertragung

>[!note] Analoge Übertragung
Die Analoge Übertragung mittels Modems und Integrated Services Digital Network (ISDN) ist veraltet.

## Point-to-Point Protocol
*Point-to-Point Protocol (PPP)*, welches die Authentifizierung mittels Usernamen und Password überprüft und daraufhin werden Netzwerkdetails zwischen Einwahlknoten des ISP und des Routers verhandelt, sowie eine IP-Adresse zugewiesen.  
PPP operiert auf [[(OSI) Open Systems Interconnection-Modell#2. Datensicherungsschicht (Data Link, Layer 2)|Layer 2]].

Und ist für die Fehlererkennung, die Aushandlung  von Verbindungsparametern und die Authentifizierung über das Link Control Protocol (LCP) zuständig.

Die Authentifikation erfolgt über das Password Authentification Protocol (PAP) oder das Challenge Handshake Authentication Protocol (CHAP).

**PPP over Ethernet (PPPoE)**
PPPoE wird benutzt um bei DSL eine Verbindung zwischen dem DSL Modem und dem ISP herzustellen indem eine virtuelle PPP Einwahl durchgeführt wird.

**PPP Tunneling Protocol (PPTP)**
Das PPTP tunnelt PPP-Datagramme und ermöglicht gesicherte Verbindungen.

**Layer 2 Tunneling Protocol (L2TP)**
L2TP ([RFC 2661](https://www.rfc-editor.org/info/rfc2661/)) ist ein Tunnelprotokoll wird für den Aufbau von VPNs benutzt. 

>[!note]
>Ein Firewall muss UDP Port 500 und 4500 und das Encapsulation Security Payload (ESP) Protokoll Nummer 50.
## Digital Subscriber Line (DSL)
Bei xDSL werden meistens bestehende Kupferleitungen der Telefongesellschaften benutzt. 
Zum Anschließen von DSL wird an den TAE-Anschluss ein *Splitter* angeschlossen, der hochfrequente DSL-Signale und die niedrigfrequenten normalen Telefonsignale voneinander trennt.

Für den Ausgang der DLS Signale wird an eine RJ-11 Twisted-Pair-Buchse ein DLS-Modem angeschlossen, welches wiederum per USB oder Ethernet Kabel mit dem Computer verbunden.
Wird statt RJ-11 Ethernet verwendet, kommt das PPPoE  zum Einsatz.

Eingesetzt wird das *Discrete Multi Tone (DMT)* Modulationsverfahren, es verwendet *Bins*, schmale Hochfrequenz-Bänder, mit je 4,3125 kHz Bandbreite um die Datenübertragung zu verteilen.

>[!note]
>Der Begriff Modem ist im Kontext von DSL falsch, da keine Analog-Digital-Umwandlung stattfindet.

Anstatt von DSL-Modems werden auch DSL-Router benutzt die statt einzelnen Rechnern mehrere Geräte anschließen können, zusätzlich kann in diesen Routern ein internet Splitter verbaut sein. 

**Asymmetric DSL (ADSL)**
Bei ADSL sind die Download und Upload Raten unterschiedlich.
Es unterstützt Breitband-Datenübertragungen im Mbit/s Bereich:
- ADSL (ITU-T G.992.1): 
  max. Upstream: 1,0 MBit/s
  max. Downstream: 10 Mbit/s
- ADSL2+ (ITU-T G.992.5)
  max. Upstream: 3,5 MBit/s
  max. Downstream: 25 MBit/s

**Symmetric DSL (SDSL)**
Bei SDLS sind Upload und Download Raten gleich.

**Very High Bitrate DSL (VDSL)**
Schnellste DSL Variante
VDSL2 nutzt Vectoring um wechselseitige Störungen zu eliminieren.

## SDH/SONET
SDH/SONET wurde 1988 als Standard definiert, wobei zwischen europäischen ETSI-SDH und nordamerikanische ANSI-SDH unterschieden wird.
Beide operieren auf [[(OSI) Open Systems Interconnection-Modell#1. Physische Schicht (Physical, Layer 1)|Layer 1]] des OSI Modells.

**Synchronous  Digital Hierarchy (SDH)**
SDH beschreibt die Struktur von Übertragungsrahmen auf Multiplexsystemen und die Normung von Funktionen, wodurch alle SDH-Netze und Systeme kompatibel sind.

**Synchronous Optical Network (SONET)**
SONET ist die amerikanische Variante von SDH.