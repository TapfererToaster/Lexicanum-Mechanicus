# Network Interface Card (NIC)
*NICs* besitzen eine oder mehrere Schnittstellen zwischen dem Rechner und dem Übertragungsmedium ([[Cables, Connectors and Ports|TP/LWL-Kabel]], Radiowellen), womit der Zugriff auf das Netzwerk möglich ist. 
Das Interface ist entweder auf dem Motherboard oder als Erweiterungskarte vorhanden.
Meistens sind NICs *bootfähig*, sie besitzen eine [[BIOS-UEFI|BIOS]] Erweiterung, die es ermöglicht ein Betriebssystem über das Netzwerk zu booten.
Eine NIC unterstützt mehrere Übertragungsgeschwindigkeiten, wobei Geräte per Autonegotiation die maximale Geschwindigkeit aushandeln und bei Bedarf auch automatisch auf eine geringere umschalten.

Jede NIC wird durch eine weltweit eindeutige [[(OSI) Open Systems Interconnection-Modell#MAC Addresses|MAC Adresse]] identifiziert. 

**Bindung**
Damit der Datenaustausch möglich ist muss die NIC an einen Protokoll-Stack gebunden werden,  wodurch diese mit den Schichten des Stacks kommunizieren kann. 
- *Open Data Link Interface (ODI)*
  Von Novell und Apple entwickelt; wird in Netware Netzen eingesetzt
- *Network Device Interface Specification (NDIS)*
  Von 3Com und Microsoft entwickelt; wird in Windows Netzen eingesetzt

>[!note]
>Eine NIC kann mehrere Protokoll Schnittstellen haben.

# Peripheral Component Interconnect | Express (PCI | e)
*PCI* ist ein Bussystem, das die Verbindung von Hardware an Steckplätzen auf dem Motherboard ermöglicht.
Die Daten werden parallel übertragen.

*PCIe* ersetzte PCI.
Daten werden nicht parallel, sondern über eine *Lane*, welche Voll-Duplex Kommunikation erlaubt.
Der Datenfluss wird von einem internen Switch auf dem Motherboard gesteuert.

# Universal Serial Bus (USB)
USB wird universell zum Anschließen von Peripherie Geräten an Computer benutzt. 
USB ist Hot-Plug und Plug & Play fähig, Geräte können also während dem laufenden Betrieb des Computers angeschlossen und entfernt werden, sowie automatisch erkannt und benötigte Treiber werden automatisch heruntergeladen.