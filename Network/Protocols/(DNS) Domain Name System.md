*Domain Name System (DNS)* is responsible for mapping a domain name to an IP address. It operates at the [[(OSI) Open Systems Interconnection-Modell#7. Anwendungsschicht (Application, Layer 7)| Layer 7 (Application)]] of the OSI model and uses UDP port 53 and TCP port 53 as a fallback.
There are many different types of DNS records:
- **A record**: maps a hostname to one or more [[IPv4]] addresses, f.e. `example.com` to `172.17.2.172`
- **AAA record**: maps a hostname to one or more [[IPv6]] addresses
- **CNAME (Canonical Name) record**: maps a domain name to one or more other domain names, f.e. `www.example.com` to `example.com` or `example.org`
- **MX (Mail Exchange) record**: specifies the mail server responsible for handling emails for a domain.

This means that when you type `example.com` in your browser, it tries to resolve this domain name by querying the DNS server for the *A record* and when you try to send an email to `test@example.com`, the mail server queries the DNS server for the *MX record*.

>[!note]
>On Unix systems a local list of names and IP addresses is stored in `/etc/hosts`, if the searched name entry is found in this file the PC will not refer to a name server.
>The most used software is *Berkley Internet Name Domain (BIND)*.

# Hierarchy
![[DNS-Hierarchy.png|514]]
Die oberste Ebene der Hierarchy ist eine spezielle Zone mit einem leeren String als Name, der durch die Root-Nameserver der ICANN verwaltet wird und erhält Verweise auf alle Top-Level-Domains.

Es gibt zwei organisatorisch Arten von Top-Level-Domains, zwischen denen es technisch keine Unterschiede gibt.
- *Generic Top-Level-Domains*
  allgemeine TLDs wie `.org` oder `.com`
- *Country Top-Level-Domains*
  Länder Domains wie `.de` oder `.us`

Unter den TLDs sind die Second-Levels-Domains wie zum Beispiel `.ac.uk` für Universitäten und `.org.uk` für Vereine und Organisationen im Vereinigten Königreich.

>[!note]
>Aus Sicherheitsgründen sollten die Zonendaten für die Domains eines einzelnen Betreibers auf mindestens zwei voneinander unabhängigen (in verschiedenen autonomen  Systemen) Namenservern vorliegen. Die Daten müssen auf dem primären *Master-Nameserver* bezeichnet werden und werden automatisch auf dem *Slave-Server* repliziert.
>Bei größeren Unternehmen und Institutionen befindet sich der externe Slave-Nameserver bei dem zuständigen Backbone-Provider.
# Nslookup
If you want to look up the IP address of a domain from the command line, you can use `nslookup`
```
nslookup google.com

Server:  unifi.localdomain
Address:  192.168.11.1

Nicht autorisierende Antwort:
Name:    google.com
Addresses:  2a00:1450:4001:81c::200e
          142.250.186.142
```

# Ablauf
![[DNS ablauf.png]]

Wenn Sie also die Website „www.beispiel.de“ aufrufen wollen geschieht folgendes:
1. Ihr Computer überprüft seinen lokalen Cache, ob ein Eintrag zu der Webseite vorhanden
ist, etwa weil sie diese schon vor kurzem aufgerufen haben. Falls es hier keinen Eintrag
gibt, wird eine (rekursive) DNS-Anfrage an den konfigurierten DNS-Server gestellt.
2. Der DNS-Server wird meistens von einem Internet Service Provider bereitgestellt, man
kann aber auch selbst einen auswählen. Dieser überprüft ebenfalls seinen Cache nach
einem Eintrag zu dieser Webseite, wird er ebenfalls nicht fündig stellt er eine (iterative)
Anfrage an einen DNS Root Server.
3. Die Root Server sind die oberste Instanz im DNS-System und leiten Anfragen zu den
richtigen Top-Level-Domain Servern weiter.
In unserem Fall wird die Anfrage nach „www.beispiel.de“ mit einem Verweis auf den
TLD-Server, der für die Domäne „.de“ zuständig ist, beantwortet.
4. Der TLD-Server besitzt Einträge über die sogenannten „Nameserver“ oder auch
autoritativen Server, die für die gesuchte Domäne, „beispiel.de“, zuständig sind und
weist den DNS-Server an diesen weiter.
5. Die autoritativen Server haben nun endlich die Einträge der IP-Adressen zum DomänenNamen. Der gesuchte Eintrag wird nun vom autoritativen Server an den DNS-Server
gesendet, dieser speichert den Eintrag in seinem Cache und sendet ihn schließlich an
ihren Rechner.
6. Nun kann ihr Rechner die gewünschte Webseite aufrufen.