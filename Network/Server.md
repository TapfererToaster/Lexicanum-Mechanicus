# Zentralisierung
## Server-Client
In einem *Client-Server* Netzwerk wird zwischen zwei Rollen unterschieden:
- *Server*
Software welche zentral anderen Rechnern Ressourcen und Funktionen zur Verfügung stellt
- *Client*
Software welche die Dienste des Servers in Anspruch nimmt

>[!note]
>Server and clients are not specific devices, they are roles and many devices can act as both, depending on the context.
>
>Although the term server is also used to refer to powerful computers, these are specifically designed and manufactured act as a server.

>[!info]
>Clients and servers are often called *endpoints* or *hosts*, as they are devices that communicate over the network.
>Opposed to network infrastructure devices, which connect the endpoints and facilitate their communication.
## Peer-to-Peer
In einem *Peer-to-Peer* Netzwerk können alle Rechner Ressourcen und Funktionen anderen zur Verfügung stellen.
# Arten von Servern
## Fileserver
Dieser Server stellt Clients bestimmte freigegebene Verzeichnisse übe das Netzwerk zur Verfügung. Oft sind sie an ein bestimmtes Betriebssystem oder eine Plattform gebunden, da diese genauso wie ein lokales Dateisystem benutzt werden sollen.
>[!note]
>Besonders wichtig ist die Verwaltung von Zugriffsrechten.
## Printserver
Dieser Server stellt Clients den gemeinsamen Zugriff auf einen Drucker bereit, sowie die passenden Druckertreiber damit diese nicht lokal auf das Client-Rechner installiert werden müssen.
## Mailserver
Dieser Server wird zum senden und empfangen von [[Email|E-Mails]] benutzt.
## Webserver
Dieser Server stellt Clients auf Anfrage Webseiten zur Verfügung die in einem Browser angezeigt werden. Diese Webseiten befinden sich als HTML Dateien statisch auf dem Server.
## Verzeichnisserver
Verzeichnisse sind datenbankähnliche Kataloge von User-Accounts, Computern, Peripheriegeräten, Diensten und Berechtigungen in einem Netzwerk. Diese Verzeichnisse können dann aufgerufen werden und von anderen Diensten benutzt werden für:
- automatisierte Softwareverteilung und -installation
- mobile Benutzerprofile (Roaming User Profiles)
- zentralisierte Anmeldedienste (Single-Sign-on)
- rechner-. benutzer- und eigenschaftsbasierte Rechtekontrolle
## Anwendungsserver und Serveranwendungen
Dieser Server erlaubt Clients die Benutzung von Anwendungsprogramme.

In der einfachsten Form sind die Daten der Anwendung auf dem Server gespeichert und die Anwendung wird in den Arbeitsspeicher des Clients geladen und lokal ausgeführt, wobei die Anwendung wissen muss, dass Komponenten und Konfigurationsdateien nicht lokal sondern auf dem Server gespeichert sind.
Die Anwendung kann, aber auch zum Teil oder vollständig auf dem Server ausgeführt werden und der Client kann über eine Bedienoberfläche (*Frontend*) mit dem Programm (*Backend*) interagieren.

Des Weiteren gibt es *verteilte Anwendungen*, die aus einem oder mehreren Datenbankservern, einem Anwendungsserver und Diversen Frontends bestehen.

## Domänencontroller