# Bestandteile
## Kernel
Der Kernel wird beim *Booten* eines Betriebssystem geladen und ausgeführt und ist das grundlegende Computerprogramm, dass unmittelbar vom Prozessor ausgeführt wird und bis zum herunterfahren des Computers permanent im Hintergrund läuft. 
Er steuert steuert alle anderen Betriebssystemkomponenten, er initialisiert die Zusammenarbeit mit der Hardware durch laden der Gerätetreiber; er ruft alle anderen Programme als Unterprogramme auf und bestimmt durch Rücksprungpunkte wann diese die Kontrolle zurück an den Kernel geben.
### Kernelmodus
Bei der Ausführung von Prozessen ist dabei zwischen *Benutzermodus* und *Kernelmodus* zu unterscheiden. Oft werden diese Modi durch unterschiedliche Modi des Prozessors ausgeführt, die z.B. unterschiedlich stark vor Interrupts geschützt sind.

>[!note]
>Der Modus mit dem höchsten Schutz wird gewöhnlich als Kernelmodus verwendet und der mit dem geringsten Schutz als Benutzermodus.

- **Kernelmodus**
  Im Kernelmodus besitzen Prozesse mehr Privilegien und erledigen deswegen Betriebssystemaufgaben, wie die Verarbeitung von Hardware-Interrupts, das Öffnen und Schließen von Dateien oder die Speicherverwaltung. Diese Prozesse können nicht von außen unterbrochen werden jedoch können sie den *Task Scheduler*, ein Prozess im Kernelmodus der die Rechenzeit auf die anderen Prozesse verteilt, aufrufen und die Kontrolle an ihn abgeben.

- **Benutzermodus**
  In diesem Modus besitzen die Prozesse weniger Privilegien und sie können durch Interrupts oder Prozesse im Kernelmodus unterbrochen werden. Durch *System Calls* können Benutzerprozess Kernelprozesse aufrufen und ermöglichen Benutzern Funktionen des Betriebssystems zu nutzen.

### Kernelarten
Es gibt zwei verschiedene Arten von Kernel, *Monolithische* und *Mikrokernel*, wobei es auch möglich ist einen Mittelweg zu gehen, indem einzelne Systeme aus dem Kernel in Subsysteme auszulagern.

- **Monolithischer Kernel**
Diese Kernelart ist die ältere der zwei Arten und führt so viele Funktionen wie möglich selber aus

- **Mikrokernel**
Diese Kernelart ist jünger und delegiert die meisten Aufgaben an Prozesse die im Benutzermodus laufen und ist vor allem für die Prozessverwaltung zuständig. Die Programme werden bei Bedarf in den Speicher geladen, der ständige Wechsel zwischen Benutzer- und Kernelmodus verbraucht jedoch Ressourcen und benötigt Zeit.
 
## Gerätetreiber
Geräte Treiber (*Device Drivers*) sind spezielle Programme die, als Schnittstelle zwischen Betriebssystem und Hardware, sich um die Steuerung einzelner Hardwarekomponenten kümmern. Die Treiber liegen meist als Module vor die bei Bedarf in den Speicher geladen und wieder entfernt werden können, sie übersetzen die Anforderungen des OS in die  Hersteller-spezifischen Steuerbefehle eines Geräts und umgekehrt.

>[!note]
>Viele Hersteller bieten selbst Treiber für ihre Geräte an, da sie ansonsten die Schnittstellen ihres Gerätes veröffentlichen müssten damit andere Treiber für das Gerät schreiben könnten.

Aus Treiber-Sicht gibt es zwei Arten von Geräten
- *Zeichengeräte (Character Devices)*
 Auf die Daten kann nur mit *sequenziellen Zugriff (Sequential Access)*, Zeichen für Zeichen, geschehen z.B. Tastatur, Netzwerkschnittstelle, Drucker
- *Blockgeräte (Block Devices)*
  Der Zugriff auf die Daten dieser Geräte kann in beliebiger Reihenfolge (*Random Access*), aber nur blockweise geschehen; z.B. CD-ROM, Festplatte, Grafikkarten.

## Systemprogramme
*Systemprogramme* werden benutzt um Dateien und Verzeichnisse zu manipulieren, Umbenennen, Löschen oder Kopieren. Steuerungs- und Analysetools gehören ebenfalls zu den Systemprogrammen. Sie können entweder durch Eingaben ihres Namen in ein Terminal oder durch Menübefehle (wie doppelklicken) in einer GUI aufgerufen und ausgeführt werden.

>[!note]
>Unix-Systeme haben sehr leistungsfähige Systemprogramme mit denen jede beliebige Verwaltungsaufgabe über die Konsole erledigt werden kann. 
>Dies ermöglicht auch eine einfache und zuverlässige Fernsteuerung von Rechnern, z.B. mithilfe von SSH.
>Bei Windows Rechnern gibt es einige Werkzeuge die nur per GUI verwendet werden können.

## Schnittstelle für Anwendungsprogramme

# Prozessverwaltung
Jede stattfindende Aufgabe wird in den meisten OS durch einen *Prozess* realisiert. Moderne Betriebssysteme sind in der Lage mehrere Prozesse parallel (*Multitasking*) auszuführen.

>[!note]
>Bei Singlecore-Prozessoren wird Multitasking durch schnelles hin- und herschalten zwischen den einzelnen Prozessen realisiert, Multicore-CPUs können jedoch tatsächlich mehrere Prozesse gleichzeitig bearbeiten  

Das Betriebssystem ist verantwortlich die Rechenressourcen auf die verschiedenen Prozesse zu verteilen. 

## Kommunikation zwischen Prozessen
Prozesse laufen völlig abgeschirmt von einander und besitzen eigene Speicherbereiche, jedoch müssen Prozesse in manchen Fällen miteinander kommunizieren. Neben Signalen werden *Pipes* dafür verwendet, die den Output eines Prozesses mit dem Eingang eines anderen verknüpfen.
Die effizienteste Kommunikation erfolgt durch *Inter Process Communication (System V IPC)*. 
>[!note]
>IPC wurde mit Unix System V eingeführt und ist in fast allen Unix und Linux Varianten verfügbar.

Bei IPC gibt es zwei Mechanismen
- *Message Queues*
  Ein Prozess kann hier hinein schreiben und andere Prozesse können daraus sequenziell lesen
- *Shared Memory*
  Speicherbereiche in die Prozesse Daten ablegt und andere Prozesse können diese beliebig oft lesen und ändern

Eine eingeschränkte Kommunikation zwischen Prozessen findet durch *Semaphore* statt, durch den mehrere Prozesse Ressourcen gemeinsam Nutzen können. Es handelt sich um einen Zähler in einem gemeinsamen Speicherbereich, der von verschiedenen Prozessen reserviert oder freigegeben werden kann. Beim reservieren wird der Zähler um 1 reduziert, vorausgesetzt er ist nicht 0, zur Freigabe wird er um 1 erhöht, bis zu einem festgelegten Maximalwert. 

## Deadlocks
*Race Condition* ist die Bezeichnung für das Wettrennen von Prozessen um den Zugriff auf Ressourcen, dieses kann zu einem *Deadlock* führen wenn die Prozesse den Zugriff auf dieselbe Datei gegenseitig sperren um selber zugreifen zu können.
Um dies zu verhindern sollte:
- Ein Prozess überprüft ob die Resource bereits gesperrt ist, falls ja gibt er die Kontrolle ab und überprüft nach einer gewissen Zeit erneut
- Ist die Ressource frei errichtet der Prozess eine Sperre 
- Benötigt der Prozess die Ressource nicht mehr, löst er die Sperre 

## Threads
*Threads* werden benutzt um Prozessen die gemeinsam dasselbe Problem bearbeiten ununterbrochen miteinander kommunizieren können. Threads besitzen keine getrennten Speicherbereiche sondern greifen auf einen gemeinsamen Speicherbereich zu.

# Speicherverwaltung
Das Betriebssystem ist auch zuständig für die Speicherverwaltung, z.B. dem Verteilen von [[Arbeitsspeicher]] an die einzelnen Prozesse. 
Aktuelle Betriebssysteme verwenden virtuell Speicheradressierung, bei der die angesprochenen Speicheradressen nicht identisch mit den Hardwareadressen des RAM sein müssen. 

> [!NOTE]
> Der virtuelle Speicherraum vom OS wird in *Segmente* unterteilt. Modernen CPUs können selber den Speicher segmentieren und haben hier für ein *Memory Management Unit*. 

Der Speicher wird in einzelne *Seiten* unterteilt die durch *Paging* auf die Festplatte ausgelagert werden, wenn sie nicht benötigt werden und zurück in den Arbeitsspeicher geladen wenn sie gebraucht werden. Diese ausgelagerten Seiten werden als *Page File* bezeichnet.

>[!note]
>Unix-Systeme benutzen häufig spezielle *Swap-Partition* Plattenpartitionen.

Die MMU benutzt eine *Seitentabelle*, die Auskunft gibt wo die virtuellen Speicherseiten sich befinden, etwa im Arbeitsspeicher oder in der Auslagerungsdatei. Wird eine Seite benötigt, wird ein *Page Fault* ausgelöst.

# Dateisysteme
Die Verwaltung von *Dateien*, benannten Einheiten die auf einem Datenträger gespeichert sind, ist ebenfalls Aufgabe des Betriebssystems. Hierfür werden von Betriebssystemen unterschiedliche *Dateisysteme* verwendet, diese greifen auf den Treiber des Datenträgers zu und organisieren die Daten auf diesem. Zusätzlich wird über ein *virtuelles Dateisystem* der Zugriff des Betriebssystems auf die verschiedenen Dateisysteme und Datenträgern vereinheitlicht.
Das Betriebssystem spricht meistens nicht direkt die Hardwaresektoren auf dem Datenträger an, sondern unterteilen diesen logisch in größere Abschnitte, *Cluster*.
Das Unterteilen in Cluster hat den Nachteil, dass eine Datei mindestens ein Cluster belegt und ein ganzes weiters Cluster wird belegt, wenn die Datei auch nur ein Byte zu groß ist.

>[!note]
>Dateisysteme wie ext3 und ext4 speichern die überstehenden Daten von Dateien in einem Cluster.

- *File Allocation Table (FAT)*
  In einer Tabelle wird die Nummer des ersten Clusters, bei dem eine Datei beginnt, gespeichert. Jede Zuordnungseinheit enthält einen Verweis auf das nächste Cluster der Datei, da diese oft verstreut und nicht zusammenhängend sind. 

  >[!note]
  >Festplatten fragmentieren mit der Zeit, da beim Löschen von kleinen Dateien Lücken entstehen, die dann mit Teilen von größeren Dateien gefüllt werden. Es ist daher wichtig bei FAT-Dateisysteme die Datenträger regelmäßig mit geeigneter Software zu defragmentieren.
  
	- *FAT16*
	  Die maximale Anzahl von Clustern auf einer Partition sind 65.536, da es ein 16 Bit Systems ist und eine Partitionsgröße von 2 GiB.
	- *FAT32*
	  32 Bit System, mit einer maximalen Cluster Anzahl von über 4 Millionen und einer Partitionsgröße von bis zu 4 TiB
	- *Extended FAT (exFAT)*
	  besonders für externe Festplatten und USB-Sticks geeignet; unterstützt größere Datenträger und Partitionen besser als FAT32 
	  
- *New Technology File System (NTFS)*
  Proprietäres Dateisystem von Microsoft
  Die Cluster werden nicht in einer Tabelle, sondern in einer komplexen Baumstruktur, die schnellere Zugriffe und mehr Schutz vor Fehlern bietet. Partitionen können komprimiert und verschlüsselt werden. Es ist möglich FAT-Systeme in NTFS zu konvertieren, jedoch nicht andersrum.
