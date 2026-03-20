#CCNA 
# Types
## Local Area Network (LAN)
>[!important] Defintion
>A group of interconnected devices in a limited area, such as an office.

![[LAN Topology.png]]
In the example above you can see that the network is split into three different LANs. You can also see that the [[Router]] is responsible for connecting different networks, while [[Switches]] connect the devices inside a LAN.
>[!note]
>Another term for a LAN is a *[[(OSI) Open Systems Interconnection-Modell#2. Datensicherungsschicht (Data Link, Layer 2)|Layer 2 domain]]*, as the data is switched using the MAC address, without the Router.

## Metropolitan Area Network (MAN)
Umfasst eine Stadt, Gemeinde oder Region in einem Umkreis von 100 km und mehr.

## Wide Area Network (WAN)
Umfasst mehrere Städte, eine Region oder ein ganzes Land.
### Datenfernübertragung
Die Datenfernübertragung basiert auf dem *Point-to-Point Protocol*, welches die Authentifizierung mittels Usernamen und Password überprüft und daraufhin werden Netzwerkdetails zwischen Einwahlknoten des ISP und des PCs verhandelt, sowie eine IP-Adresse zugewiesen.  
>[!note]
>Die schon in den 1980er Jahren verlegten Glasfaserkabel für Kabelfernsehen verlegt wurden, besaßen in der ursprünglichen Version keine Rückkanalfähigkeit, es konnten also nur Daten empfangen nicht aber gesendet werden.
#### Digital Subscriber Line (DSL)
Bei DSL Leitungen werden meistens bestehende Kupferleitungen der Telefongesellschaften benutzt. 
Zum Anschließen von DSL wird an den TAE-Anschluss ein *Splitter* angeschloßen, der hochfrequente DSL -Signale und die niedrigfrequenten normalen Telefonsignale voneinander trennt.
Für den Ausgang der DLS Signale wird an eine RJ-11 Twisted-Pair-Buchse ein DLS-Modem angeschloßen, welches wiederum per USB oder Ethernet Kabel mit dem Computer verbunden.

>[!note]
>Der Begriff Modem ist im Kontext von DSL falsch, da keine Analog-Digital-Umwandlung stattfindet.

Wird statt einer RJ-11 Ethernet verwendet, kommt das PPP over Ethernet (PPPoE) Protokoll zum Einsatz.

Anstatt von DSL-Modems werden auch DSL-Router benutzt die statt einzelnen Rechnern mehrere Geräte anschließen können, zusätzlich kann in diesen Routern ein internet Splitter verbaut sein. 
**Asymmetric DSL (ADSL)**
Bei ADSL sind die Download und Upload Raten unterschiedlich.

**Symmetric DSL (SDSL)**
Bei SDLS sind Upload und Download Raten gleich.

## Global Area Network (GAN)
Umfasst mehrere Länder, einen Kontinent oder die ganze Welt.
# Topology
Die Topologie eines Netzwerkes beschreibt in welcher physikalischen Grundform die einzelnen Geräte organisiert sind.
## Bustopologie
Bei einer Bustopologie werden die Geräte hintereinander an einen Kabelstrang angeschloßen. Die Enden des Kabelstrangs werden mit Abschlußwiderständen (Terminatoren) abgeschloßen. 

## Sterntopologie
Bei einer Sterntopologie werden die Geräte an ein zentrales Gerät angeschloßen, oft ein [[Switches]].

## Ringtopologie
Bei einer Ringtopologie werden die Geräte an einem Kabelstrang ringförmig angeschloßen, wobei die Enden des Kabelstrangs nicht terminiert werden sondern einen geschloßenen Ring bilden.

## Baumtopologie
Bei einer Baumtopologie gehen von einem Gerät aus mehrere Verästelungen ab, an denen sich weitere Geräte oder Netze befinden.
