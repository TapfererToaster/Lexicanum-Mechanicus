Firewalls can be dedicated devices or software applications that protect the network or host device, by allowing or blocking certain network traffic.
>[!note]
>Firewall software like Microsoft Defender are known as *host-based firewalls*.
>A dedicated firewall device is called a *network firewall*.

Anhand des Funktionsumfangs einer Firewall kann diese Daten der Layer 2 bis 7 des OSI Modells filtern.
Dabei werden eine von drei Aktionen ausgeführt:
- Allow: Die Daten werden durch gelassen
- Deny: Die Daten werden verworfen und der Sender enthält eine "Time Out" Nachricht
- Reject: Die Daten werden verworfen und der Sender enthält eine Fehlermeldung

**Stateful und Stateless**
Stateful Firewalls prüfen den Inhalt von Datenpaketen und können das Verhalten dieser untersuchen und kategorisieren. Die Firewall kann auch auf Ereignisse regieren die nicht von einem Administrator konfiguriert wurden.

Stateless Firewalls prüfen die Quell, das Ziel oder andere Eigenschaften eines Pakets um dieses als Bedrohung einzustufen oder nicht. Die zu überprüfenden Parameter müssen von einem Administrator oder dem Hersteller konfiguriert werden, anderes wird blockiert. 

**Paketfilter**
Paketfilter sind eine einfache Firewall, die Header von Layer 3 Protokollen (IP, ICMP) oder Layer 4 Protokollen (TCP,UDP) überprüfen.
Die verhindert nicht Fragmentierungs Attacken oder Buffer Overflow.

**Stateful Inspection Firewall**
Stateful Inspection Firewalls ist eine Weiterentwicklung von Paketfiltern und kann aktuelle Status und Kontextinformationen speichern und diese bei der Filterung zu berücksichtigen.
So können z.B. nur Antwort Pakete auf Anfragen aus dem Intranet zugelassen werden, wodurch Fragmentierungs Attacken verhindert werden können. Zusätzlich können Denial of Service (DoS) Attacken verhindert werden, indem die Anzahl von Verbindungsversuchen auf eine bestimmt Anzahl pro Sekunde begrenzt wird.

**Application Level Firewalls (ALF)**
Eine ALF arbeitet auf Layer 7 des OSI-Modells und steht als Proxy zwischen Client und Server.
Hier wird die komplette Datenkommunikation bis zum Layer 7 überwacht.

**Weitere**
- Transparent Firewall:
  Stateful Inspection Firewall, welche transparent im Netz auftritt, so erscheint sie als Router ohne dahinterliegendes Netzwerk
- Personal / Desktop Firewall
  Ist als Software auf Endgeräten installiert oder im Betriebssystem integriert und ist eine Mischung aus Paketfiltern und Stateful/-less Firewall.
- Application Inspection / Next Generation Firewall
  Untersucht Daten und Pakete auf dem Application Layer und kann Richtlinien auf dieser und Nutzerebene umsetzen.
- Unified Threat Management (UTM)
  Zentrale Sicherheit für das gesamte Netzwerk, indem verschiedene Funktionen wie Intrusion Detection Systems, Contentfilter, sowie Virus-, Spam-, und Surfprotection in einem Gerät untergebracht werden. 