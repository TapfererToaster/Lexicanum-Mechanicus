> [!NOTE]
> [Windows Server | Microsoft Learn](https://learn.microsoft.com/de-de/windows-server/get-started/)

# Netzwerk
**DHCP**
Damit ein DHCP Dienst starten kann muss er im Active Directory autorisiert werden um.

**DNS**
DNS spielt bei Windows Server eine zentrale Rolle und ist eine Voraussetzung damit Active Directory funktioniert. Unteranderem ermöglicht es die Benutzeranmeldung durchzuführen.
# Dateisystem
**Distributed File System**
DFS ermöglicht es eine Verzeichnisstruktur für die Daten einer Organisation oder Firma zu erstellen.

**NTFS-Datenträgerkontingente**
Diese können Kontingente auf Speicherplatz verwalten, dadurch kann man Benutzern einen festen Speicherplatz zugewiesen werden. 
Dabei gibt es:
- *harte Quotas*: 
  der Speicherplatz ist fest begrenzt, ein Überschreiten der Grenze ist nicht möglich
- *weiche Quotas*:
  bei Überschreiten der Quota kommt es zu einer Warnmeldung

**Ressourcen-Manager**
Der Ressourcen Manager ermöglicht es festzulegen, welche Dateitypen wo gespeichert werden dürfen. Sollte ein Benutzer versuchen einen verbotenen Dateitypen zu speichern, kann unter anderem die Speicherung verboten werden oder es wird eine Benachrichtigung an den Administrator versendet.

**Datenträgerdeduplizierung**
Die Datenträgerdeduplizierung erfasst Dateien die mehrmals auf einem Datenträger vorhanden sind und erfasst binär die Daten und Unterschiede. Die Unterschiede der Dateien wird für jede Version gespeichert, wodurch sich die Datenmenge reduzieren lässt.

**NTFS**
[[Betriebssysteme - Operating Systems#New Technology File System (NTFS)|NTFS]] ist das standard Dateisystem von Windows Betriebssystemen.

**ReFS**
Das *Resilient File System* ist ein, mit Windows Server 2012 erschienenes, Dateisystem, das vor allem für die Bereitstellung von Dateien in einem Netzwerk spezialisiert ist. 
Es wird parallel zu NTFS eingesetzt, soll diese auf lange Sicht aber ersetzen.
ReFS unterstützt jedoch nicht einige Besonderheiten von NTFS, wie etwa shadow copies.
Es ist in der Lage defekte Dateien automatisch zu reparieren und ist unempfindlicher gegenüber Abstürzen des Betriebssystems oder plötzliches Ausschalten des Servers.
# Erstkonfiguration
## Computername und Arbeitsgruppe/Domäne 
Im Servermanager können diese Informationen geändert werden:
- Computername:
  Der Computername muss einmalig in der Domäne/Arbeitsgruppe sein
- Arbeitsgruppe/Domänenname:
  max. 15 Zeichen; darf nur aus englischen Buchstaben, Ziffern und Bindestrichen bestehen

Die Änderungen werden erst nach einem Neustart aktiv.

  Falls der Server einer bestehenden Domäne beitreten soll gibt man den Domänennamen ein und:
  - die IP-Konfiguration des Servers muss stimmen und mit einem passenden DNS-Server konfiguriert sein
  - Ein Computerkonto muss vorbereitet sein oder ein Benutzerkonto, das Computer der Domäne hinzufügen kann (Standardeinstellungen: jeder Domänenbenutzer 10 Computer einer Domäne hinzufügen)

## IP konfigurieren
>[!note]
>Die aktuelle IP-Konfiguration kann mit dem Befehl `ipconfig /all` angezeigt werden

## Neues Administratorkonto
Es ist empfohlen nicht mit dem Standardkonto Administrator zu arbeiten, sondern ein neues Konto mit Administratorrechten zu erstellen.
- Systemsteuerung > Benutzerkonten > Anderes Konto verwalten
- Klicken auf Benutzerkonto hinzufügen 
- Eingabe der Daten
- Auf das Konto klicken > Kontotyp ändern
- Klicken auf Administrator > Kontotyp ändern

# Server-Manger
Der Server-Manger ist die zentrale Verwaltungsplattform es dient der Überwachung und Einstellung der vorhandenen Server, sowie der installation von neuen Rollen (DNS, Hyper-V, Domänencontroller, ...) und Features (Bitlocker, BranchCache)
# Hyper-V
Hyper-V ist ein [[Virtualization#Hypervisors|Hypervisor]] von Microsoft und ist bei Windows Server und Windows Pro bereitgestellt.

Bevor man Hyper-V installiert, sollte überprüft werden ob die Data Execution Prevention (DEP) aktiviert ist. 
Dafür wird der folgende Befehl im Terminal ausgeführt:
```
wmic OS get DataExecutionPrevention_SupportPolicy
```

Die Rückgabe ist ein Wert zwischen 0 und 3, nur bei dem Wert 0 muss DEP im BIOS aktiviert werden.

| Wert | Status                                                          |
| ---- | --------------------------------------------------------------- |
| 0    | DEP ausgeschaltet                                               |
| 1    | für alle Software eingeschaltet                                 |
| 2    | Nur für Systemkomponenten eingeschaltet                         |
| 3    | für alle Software eingeschaltet, Admin kann Ausnahmen erstellen |
## Installation

Man muss schauen ob bei der CPU Virtualisierung (Intel VT-x/AMD-V) unterstütz wird
Dafür muss im BIOS die passenden Optionen angepasst werden.
Sollte der Server auf einem Proxmox sein Host muss zusätzlich Optionen für nested virtualisation aktiviert werden (unter VM > Hardware > Processor)

- Öffnen des Server-Manager > Lokaler Server (falls Rolle auf lokalem Server installiert werden soll)
- In Taskleiste auf `Verwalten` > `Rollen und Features hinzufügen`
- `Rollenbasierte Installation` > `Serverauswahl` 
- Unter `Serverrolle` > `Hyper-V`
- `Virtuelle Switche` auswählen oder leer lassen (kann später geändert werden)

>[!note]
>Unter `Standardspeicher` sollte man bei mehreren Festplatten die schnellste auswählen.

## Einrichten

Um den Hyper-V-Manager aufzurufen kann man im Server-Manager unter Tools > Hyper-V-Manager auswählen, oder im Startmenü Hyper-V eingeben.

>[!note]
>Hyper-V verbindet sich standardmäßig mit dem lokalen Server, man kann jedoch auch eine Verbindung zu einem anderen Hyper-V Host erstellen.
>In der linken Spalte per rechtsklick auf Hyper-V Manager > Verbindung mit Server herstellen

### Virtuelle Switche
Virtuelle Switche ermöglichen den VMs miteinander, mit dem Host und dem Internet zu kommunizieren.
Es gibt drei Typen:
- *Extern*:
  Die VMs sind im Netzwerk sichtbar und haben Internetzugang
- *Intern*:
  Die VMs können miteinander und mit dem Host kommunizieren
- *Privat*:
  Die VMs können nur miteinander kommunizieren

Um einen virtuellen Switch zu erstellen klickt man auf der rechten Seite unter "Aktionen" > Manager für virtuelle Switche.

Nach der Erstellung kann man unter` Systemsteuerung > Netzwerk und Internet > Netzwerk- und Freigabecenter > Adaptereinstellungen` überprüfen ob die virtuellen Switche erkannt wurden.
- Ein externer Switch wird dann als der Netzwerkadapter für das lokale LAN und Internetzugriff erkannt und muss eine dementsprechende Konfiguration aufweisen.
- Ein lokaler Switch ist mit den VMs verbunden und sollte als Default gateway für diese eingerichtet werden.

## VMs
Nach Erstellen der VM kann man unter `Einstellungen` > `DVD-Laufwerk` Keine auswählen um die ISO Image auszuwerfen und einer anderen VM zur Installation geben.

## Prüfpunkte
Prüfpunkte sind eine Kopie des Systems zu einem bestimmten Zeitpunkt und werden eingesetzt, sollte es nötig sein zu einem Systemzustand zurückzukehren.
Um einen Prüfpunkt zu erstellen wählt man die jeweilige VM aus und benutzt den Punkt `Prüfpunkt`.

# Active Directory
