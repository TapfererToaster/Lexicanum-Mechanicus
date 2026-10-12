Active Directory ist ein Verzeichnisdienst von Microsoft, womit Ressourcen hierarchisch gespeichert, identifiziert zugänglich gemacht werden.
Die dazugehörige Datenbank orientiert sich am [X.500 Standard](https://en.wikipedia.org/wiki/X.500) und für Abfragen wird das [*Lightweight Directory Access Protocol (LDAP)*](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol) benutzt.

# Domäne, Struktur und Gesamtstruktur
AD ermöglicht es mithilfe von Objekttypen, wie Benutzer, Gruppe oder Computer, die Struktur eines Unternehmens abzubilden. 
Dafür müssen jedoch die Firmenstruktur, die Geschäftsbereiche, sowie logischen Zusammenhänge zwischen Geschäftsprozessen, Abhängigkeiten und Hierarchien, Funktionen und Aufgabenteilung untersucht werden.

**Domäne**
Eine *Domäne* ist ein zentralverwalteter Bereich im Active Directory.
Um eine Domäne zu erstellen wird ein Domänencontroller installiert, welcher alle Objekte in der Domäne speichert.

**Struktur**
![[AD Struktur.png|200x188]]
Eine *Struktur* oder auch *Tree* entsteht wenn einer AD Domäne weitere Subdomänen hinzufügen, welche den Namen der übergeordneten Domäne zugeordnet werden.
z.B. Domäne `Firma.intern`, Subdomäne `Vertrieb.Firma.intern`

**Gesamtstruktur**
![[AD Gesamtstruktur.png|352x212]]
Eine *Gesamtstruktur* entsteht wenn im AD weitere Domänen mit anderem Namen hinzugefügt werden, wodurch die Domänen neben und nicht untereinander liegen.
z.B. `Firma.intern`, `GmbH.intern`
 
##  Vertrauensstellungen
Zwischen Domänen werden Vertrauensstellungen gebildet, durch die es ermöglicht wird, dass Benutzer einer *trusted domain* auf Ressourcen einer *trusting domain* zugreifen können.

**Bidirektionale, transitive Vertrauensstellungen**
Innerhalb einer Struktur entstehen Vertrauensstellungen bidirektional und transitiv (selbstfortsetzend). 
Dadurch können sich alle Benutzer in einer Struktur auf allen Geräten in den einzelnen (Sub)domänen anmelden und auf Ressourcen zugreifen.

**Unidirektionale, nichttransitive Vertrauensstellungen**
Zwischen Domänen die nicht zur selben Struktur gehören werden unidirektionale und nichttransitive Vertrauensstellungen erstellt, wodurch der Ressourcen Zugriff nur in einer Richtung geht.

# Funktionsebenen
Über die Funktionsebenen wird festgelegt, welche Funktionen und Betriebssystem-Version für Domänencontroller verfügbar sind. 

>[!note]
>Die OS Version der DCs darf nicht niedriger als die Gesamtfunktionsebene sein, so kann ein in einer Gesamtfunktionsebene Windows Server 2022, ein Windows Server 2008 nicht zu einem DC konfiguriert werden.

>[!warning]
>Während der AD-Installation wird die Domänen- und Gesamtfuntionsebene ausgewählt, diese kann später nicht mehr runtergestuft werden und sollte beachtet werden wenn unterschiedliche Server Versionen verwendet werden.
>

Um die Gesamtstrukturfunktionebenen zu erhöhen wird das MMC-Snap-In `Active Directory-Domänen und -Vertrauensstellungen.`

Klick per rechtsklick auf das Snap-In und wähle den Eintrag, dort kann die Domänenfunktionsebne heraufgestuft werden; im AD-Verwaltungscenter kann das ebenfalls geändert werden.

Um die Gesamtstrukturfunktionsebene herauf zu stufen, müssen alle Domänen die entsprechende Funktionsebene haben.  

# Domänencontroller
Domänencontroller übernehmen Verwaltungsaufgaben innerhalb der Domäne, weswegen es sinnvoll ist über mehrere zu verfügen um die Ausfallsicherheit zu erhöhen.
Bei Veränderungen müssen alle DC informiert und die Änderungen übertragen werden, dieser Prozess wird *Replikation* genannt.

## Flexible Single Master Operation (FSMO)
Der *FSMO* oder auch Betriebsmaster genannt, ist eine Funktion die nur einem DC zugewiesen werden kann.
Die Rollen sind:
- *Infrastruktur-Master*:
  Sichert die korrekte Namenszuordnung bei domänenübergreifenden Gruppenmitgliedschaften
- *Relative ID (RID) Master*:
  Sichert die Eindeutigkeit von Domänen Objekten sicher, durch SID Generierung
- *Primärer DC (PDC) Emulator*:
  Verantwortlich für Kennwortänderungen und eine zentrale Zeitangabe für all Domänen Computer
- *Schema Master*:
  Kann Veränderungen am Schema ausführen
- *Domain-Name Master*:
  Stellt sicher, dass bei dem Löschen oder Erstellen neuer Domänen, das AD in einem funktionierenden Namensraum arbeitet


>[!note]
>Der Powershell Befehl `Get-ADDomain-Controller` benutzt werden um Infos über die DC zu erhalten
>Um einen Überblick über die Betriebsmaster zu erhalten kann in der Powershell folgender Befehl eingegeben werden
>`netdom query fsmo`

**Verwaltung und Verteilung**
Standardmäßig erhält der erste DC einer Gesamtstruktur alle FSMO Rollen und dem ersten DC einer Domäne werden die drei domänenweiten Funktionen PDC Emulator, RID Master und Infrastrukturmaster zugewiesen.

Die Empfehlung für die Verteilung der Rollen:
- Infrastruktur-Master sollte nicht auf einem globalen Katalog liegen, da sonst Probleme bei der Auflösung von Gruppen, mit Mitglieder aus verschiedenen Domänen, auftreten können.
- Domänen Master und Schema Master sollten auf einem DC liegen, der globaler Katalog ist
- PDC Emulator und RID Master sollten auf einem DC liegen, der globaler Katalog ist. Diese Rollen kommunizieren viel miteinander.
## Global Catalog 
Der *Global Catalog (GC)* ist eine Rolle die von Domänencontrollern ausgeführt werden kann, sowie eine domänenübergreifende Suchfunktion für AD Objekte, in der Attribute aller Objekte aus allen Domänen gespeichert werden.
Diese Funktion sollte mehreren Domänencontrollern zugewiesen werden.

## Sysvol

## DNS-Einträge und Service Resource Records
Domaincontroller und ihre Dienste werden im DNS in *Service Resource Records (SRV)* identifiziert, welche automatisch erstellt werden und nach der Erstellung einer neuen Domäne überprüft werden.
- DNS aufrufen (über Suchleiste)
-  `Forward-Lookupzonen` erweitern und in dem entsprechenden Domänenordner erweitern

Die SRV Einträge werden automatisch bei jedem Start des Anmeldedienstes angelegt, falls nicht kann man die Registrierung erzwingen:
- mit dem Befehl `net stop netlogon` gefolgt von `net start netlogon`
- hinzufügen der Einträge mit `ipconfig /registerdns`

Beim hochstufen von Servern, wenn die DNS Zone vom System erstellt wurde, wird sie ins AD integriert.
Um das zu überprüfen:
- Im DNS Manager rechtsklick auf den Domänenordner
- `Eigenschaften` > Registrierkarte `Allgemein` > `Typ: Active-Directory integriert`
# Organisationseinheit (OU)
Ein *Organizational Unit (OU)* ist ein Objekt, das für folgende Zwecke benutzt wird:
- Strukturiertes Speichern von Objekten
- Delegierung von Verwaltung 
  z.B. Benutzer- und Gruppenverwaltung kann an Nicht-Administratoren delegiert werden, dadurch werden weniger Benutzerkonten mit Administratorrechten benötigt
- Zuweisen von Gruppenrichtlinien

Für eine OU-Struktur sollten einige Überlegungen getätigt werden um ein Konzept zu entwickeln:
- sinnvolle und einheitliche Benennung 

Container können keine OUs enthalten und mit Gruppenrichtlinien versehen werden, weswegen sie im MMC-Snap-IN Gruppenrichtlinienverwaltung ausgeblendet.

# Standorte 
Standorte werden verwendet wenn das AD über ein LAN hinaus geht und somit Replikation, Domänenanmeldungen und Datenverkehr standortübergreifend werden.
Dabei ist ein Standort lediglich um ein oder mehrere IP Netze die einen Namen zugewiesen bekommen.
Vorgehen
- Definieren von Standortnamen
- Verknüpfung der IP-Adressen mit den zugehörigen Standortnamen
- Verschieben von Domänencontrollern in die Standorte
- in jedem Standort sollte ein globaler Katalog verfügbar sein
- Definieren von Standortverknüpfungen und Zuweisung an Standorte

Wenn Standorte benutzt werden folgt AD Datenverkehr folgend ab:
1. Clients versuchen lokale Ressourcen zu nutzen
2. Sind die Ressourcen nicht vorhanden wird die billigste Standortverknüpfung verwendet
3. Erfolgt der Zugriff über mehrere Standortverknüpfungen werden die Kosten addiert

# Sysvol 
Der Ordner Sysvol beinhaltet Ressourcen zur Anmeldung, wie Gruppenrichtlinien oder Anmeldescripts für Benutzeranmeldung
Der Inhalt der Freigabe `SYSVOL` wird von dem *File Replication Service (FRS)* zwischen den DC einer Domäne repliziert.
Die Replikation kann auch per DFS erfolgen, dabei wird der Ordner `SYSVOL` zu `SYSVOL_DFSR`
Diese Freigaben `SYSVOL` und `NETLOGON` werden von dem Anmeldedienst `netlogon` benötigt.
Des Weiteren sind folgende Ordner enthalten
- `sysvol`:
  Verknüpfung mit dem Ordner `domain` mit identischem Inhalt
  entspricht der Freigabe `SYSVOL` und beinhaltet einen Ordner mit dem Namen der Domäne
- `stagging` / `stagging areas`:
  werden für die Verwaltung der Replikation gebraucht
- `\domain\Policies` und `\sysvol\domänenName\Policies`
  beinhalten Ordner mit Gruppenrichtlinienobjekten
- `\sysvol\domänenName\scripts`:
  entspricht der Freigabe `NETLOGON`, wo Benutzer-Anmeldeskripte gespeichert werden

# Installation
**Voraussetzungen**
- jede Windows Domäne braucht mindestens ein Windows Server
- es muss Zugang zum Netzwerk/Internet bestehen und TCP/IP muss als Netzwerkprotokoll verwendet werden
- In jeder Domäne muss ein DNS-Server vorhanden sein, der SRV Ressourceneinträge unterstützt
- weitere Domänencontroller müssen einen DNS Server abfragen können, um Domänendienste zu lokalisieren
- Server die als Domänencontroller fungieren sollen, müssen eine korrekte Uhrzeit und Zeitzone eingestellt haben
- um eine neue Domäne zu einer Gesamtstruktur oder einen Domänencontroller zu einer Domäne hinzuzufügen, werden Anmeldedaten eines Organisations- oder Domänenadministrators benötigt

## Neue Domäne einrichten
**Domänencontroller installieren**
- "`Server-Manager`"
- "`Verwalten`"
- "`Rollen und Funktionen hinzufügen`"
- Installationstyp: "`Rollenbasiert`"
- Server auswählen
- "`Active Directory-Domänendienste`" auswählen
- Bestätigen und Installieren

Die Rolle kann auch per Powershell mit folgendem Befehl installiert werden;
```
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```

**Domänencontroller hochstufen**
![[Domänencontroller hochstufen.png]]
### Neue Gesamtstruktur hinzufügen
Ein *Fully Qualified Domain Name (FQDN)* muss angegeben werden und es wird empfohlen mindestens eine Second-Level-Domain anzugeben, z.B. `firma.intern`.

Bei der Festlegung der Gesamtstrukturfunkionsebene sollte sich an der ältesten Windows Server Version der Domain Controller orientiert werden.
Diese Einstellung ist nicht umkehrbar, d.h. die Funktionsebene kann nicht herabgestuft werden.

Die Optionen `DNS-Server` und `Globaler Katalog` sollten ausgewählt sein.

Das *Directory Services Restore Mode (DSRM)* Passwort wird benötigt wenn gelöschte AD Objekte nach einem booten in den Verzeichnisdienst-Wiederherstellungsmodus gelangen sollen.
Das Passwort wird auf jedem Domain Controller lokal gespeichert und getrennt verwaltet.

> [!NOTE]
> Standardmäßig wird die Active Directory-Datenbank in einem Ordner *NTDS (NT Directory Service)* auf `C:\` abgelegt. Aus Sicherheitsgründen wird für das Active Directory-Laufwerk den Schreibcache ausschaltet, deswegen wird empfohlen einen separaten Datenträgers für den Datenbankordner zu nutzen. Die Protokolldateien sollten jedoch nicht auf dem gleichen Datenträger liegen wie die Datenbank, damit bei Ausfall der Datenbankplatte aus einer Sicherung und den Änderungsprotokollen eine aktuelle Version der Datenbank erstellet werden kann. Den Speicherort des Ordners SYSVOL sollten Sie nicht verschieben, da sich Replikationsprobleme ergeben können, wenn dieser nicht am Standardspeicherort liegt.

Nach der Erstellung der Domäne wird ein neues Domänenadministrator Konto angelegt das den Namen und Passwort des lokalen Admins übernimmt. 
Der erste Domänenadmin in einer neuen Gesamtstruktur ist der *Enterprise-Admin* oder auch *Organisations-Admin* genannt, dieser ist verantwortlich für die Gesamtstruktur der Organisation.

### Domänencontroller zu Domäne hinzufügen
- "`Domänencontroller zu einer vorhandenen Gesamtstruktur hinzufügen`"
- Angabe des Domänennamen und Anmeldeinformationen in der Form `domainName\Kontoname`
- `DNS-Server` und `Globaler Katalog` auswählen


# Tools

**Active Directory-Benutzer und -Computer**
Hier werden neue Organisationseinheiten, Benutzer, Gruppen und andere Objekte angelegt.

>[!tip]
>Im Menü `Ansicht`  sollte `Erweiterte Ansicht` ausgewählt werden

**Active Directory-Domänen und -Vertrauensstellungen**
Hier kann die Gesamtstruktur, die einzelnen Strukturen, Domänen und Unterdomänen angezeigt und Vertrauensstellungen verwaltet werden. 
Auch kann die Funktionsebene für Domäne und Gesamtstruktur heraufgestuft und der Betriebsmaster geändert werden.

**Active Directory-Modul für Windows PowerShell**
Mit diesem Modul ist es möglich Die Struktur und Funktionalität des AD mit PowerShell zu verändern.
Bei Windows Server 2022 ist es möglich remote auf den Domänencontoller zuzugreifen, jedoch sind dafür Remoteserver-Verwaltungstools, sowie die Rollenverwaltungstools/AD-DS-/AD LDS-Tools/Active Directory-Modul für Windows PowerShell nötig.
Zusätzlich muss auf dem Zielserver der Befehl  `Enable PSRemoting -Force` eingegeben werden, um automatisch Ausnahmen in der Firewall zu aktivieren.
Mit `Disable-PSRemoting -Force` kann dies deaktiviert werden.

**Active Directory-Standorte und -Dienste**
Hier können Standorte, Standortverknüpfungen und Subnetze für eine Domäne eingerichtet werden.

**Active Directory-Verwaltungscenter**
Die zentrale Verwaltungsschnittstelle, mit der Routineaufgaben erfüllt werden können.





















































