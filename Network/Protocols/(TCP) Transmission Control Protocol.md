This Protocol operates at the [[(OSI) Open Systems Interconnection-Modell#4. Transportschicht (Transport, Layer 4)|transport layer (Layer 4)]] of the OSI model and is used for reliable, connection-oriented communications. 
In order to be reliable it adds overhead und thus some inefficiencies.
TCP enables:
- Error recovery
- Flow control using windowing
- Connection establishment and termination
- Ordered data transfer
- Data segmentation

Applications that rely on TCP are:
- HTTP
- FTP
- Telnet
- SSH
- SMTP

# TCP Protocols and their Ports
[[TCP-IP Modell#Protocols and their Ports|Ports]] of TCP protocols are:

| Port | Protocol    |
| ---- | ----------- |
| 20   | FTP data    |
| 21   | FTP control |
| 22   | SSH         |
| 23   | Telnet      |
| 25   | SMTP        |
| 53   | DNS         |
| 80   | HTTP        |
| 110  | POP3        |
| 143  | IMAP        |
| 443  | HTTPS       |

# Header
![[bilder/tcp/TCP Header.png]]

- *Sequence Number*
Gibt an zu welchem Byte der zu übertragenden Sequenz das erste Nutzdatenbyte des Pakets entspricht; Ist die SYN-Flag gesetzt wird die *Initial Sequence Number (ISN)* angegeben.
- *Acknowledgement Number*
Startbyte der nächsten erwarteten Pakets; nur bei gesetztem ACK-Bit von Bedeutung
- *Header Length* / *Offset*
Anzahl der 32-Bit-Wörtern aus denen der Header besteht; 
- *Reserved*
Reserviert für zukünftige Anwendungen; muss Wert 0 haben
- *Control Bits* / *Flags*
	- *URG (Urgent Data)* 
	  Gesendete Daten sind Urgent Data; der Urgent-Pointer muss beachtet werden
	- *ACK (Acknowledgement)* 
	  die Acknowledgement Number muss beachtet werden
	- *PSH (Push)*
	  Pufferung des Pakets wird verhindert; es wird unmittelbar gesendet
	- *RST (Reset)*
	  Verbindung zurücksetzen
	- *SYN (Synchronize)*
	  Sequenznummer synchronisieren
	- *FIN (Finish)*
	  Ende der Sequenz; keine weiteren Daten vom Absender
- *Window*
Anzahl von Datenbytes die der Absender bereit ist; kann durch  *Maximum Transmission Unit (MTU)* bei manchen Schnittstellen konfiguriert werden
- *Checksum*
Wird benutzt um die Korrektheit der Daten zu sichern
- *Urgent-Pointer*
Zeigt auf das Byte der aktuellen Sequenz das Urgent Data enthält
- *Optionen*
Enthält verschiedene hersteller- und implementierungsabhängige Zusatzinformationen; (immer ein vielfaches von 8 Bit lang)


