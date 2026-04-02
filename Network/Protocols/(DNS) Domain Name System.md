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