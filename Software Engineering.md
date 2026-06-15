# Projektmanagement
Das Projektmanagement hat als Aufgabe den Projektablauf, sowie die Projektziele, Zeit und Ressourcen kontinuierlich zu überprüfen und zu managen.

>[!note]
>Nach DIN-Norm 69901 ist Projektmanagement die "Gesamtheit von Führungsaufgaben, -organisation, -techniken und -mitteln für die Abwicklung eines Projekts".

Die Aufgaben können in neun Kategorien unterteilt werden:
- *Integrationsmanagement*:
  Koordination der verschiedenen Projektbestandteile und -beteiligten
- *Umfangsmanagement* (Scope Management):
  Überwachung des Projektzustands in Bezug auf die Ziele und Vorgaben 
- *Zeitmanagement*:
  Einhaltung des Projektzeitplans 
- *Kostenmanagement*:
  Kontrolle der Projektkosten und Implementierung von geeigneten Kostendämpfungsmaßnahmen 
- *Qualitätsmanagement*:
  Sicherstellung, dass Elemente und Teilergebnisse des Projekts einem qualitativen Standard entsprechen
- *Personalmanagement / Ressourcenmanagement*:
  Verteilung des Personals und Arbeitsmittel auf verschiedene Projektteile und -phasen
- *Kommunikationsmanagement*:
  Festlegung der Kommunikationsmittel, -wege und -standards
- *Risikomanagement*:
  Notfallplanung und reagieren bei Notfällen
- *Beschaffungsmanagement*:
  Koordination von Kapazitäten, Nachbestellungen und Lieferzeiten von Arbeitsmitteln, um Warten und Verzögerungen zu vermeiden.

## Netzplan
Netzpläne werden zur Zeitplanung und -koordination benutzt, um zu bestimmen in welcher Reihenfolge die einzelnen Schritte durchgeführt werden und welche Schritte einander bedingen.
![[Netzplan.png|535x206]]

## Gantt-Diagramm
Bei einem Gantt-Diagramm, werden die Schritte durch Balken symbolisiert und deren Länge die Dauer der Schritte.
# Entwicklungsprozess

> [!NOTE]
> Die einzelnen Schritte können verschieden durchlaufen werden:
> *linear*: die Schritte werden nach einander ausgeführt und abgeschlossen (Wasserfall)
> *iterativ*: Die Schritte werden mehrfach durchlaufen (Spirale)

## Planung
Hier wird der Zweck und die Leistungen der Software bestimmt, indem diese zu einem Katalog ausgearbeitet werden.
### Lasten- und Pflichtenheft
Die Ergebnisse der Planung werden in ein *Lastenheft* (Statement of Work) gefasst, welches eventuell von Kunden oder in Zusammenarbeit mit diesen erstellt wird.
Der Inhalt ist:
- Definition des Projektziels
- Anforderungen an den Einsatz des Produkts
- allgemeine Informationen zum Produkt
- Beschreibung der Funktionen des Produkts
- Bestimmung der Leistungen, die der Auftragnehmer zu erbringen hat
- Qualitätsstandards, denen das Produkt genügen soll, wie Zuverlässigkeit, Benutzbarkeit, Effizienz und Änderbarkeit
- weitere Informationen und Anforderungen

>[!note]
>Nach Din 69905 enthält das Lastenheft die "Gesamtheit der Forderungen an die Lieferungen und Leistungen eines Auftragnehmers".

Auf Grundlage des Lastenhefts wird dann ein *Pflichtenheft* (Proposal), welches präziser die technischen Eigenschaften der Dienstleistung/Produkts beschreibt.
Inhalt ist z.B.:
- Projektziele
- Projektvorgaben
	- Hardwarebasis
	- Softwarevoraussetzungen
	- einzusetzende Arbeitsmittel
	- Nebenbedingungen
- Projektanforderungen
	- Aufgaben und Funktionen des Produkts
	- Benutzerschnittstelle
	- Lieferumfang
	- Kompatibilität und Portierbarkeit
	- Erweiterbarkeit und Änderbarkeit
- weitere Leistungen
	- geplante Testreihen
	- Qualitätssicherung
	- Support-Vereinbarungen
- Kostenkalkulation
- Literatur
### Analyseverfahren
Um einen Plan zu erstellen sollte analysiert werden, welche Probleme das Projekt lösen soll, wie es diese lösen soll und mit welchen Mitteln.

**Analyseformen**
*Systemanalyse*
Untersuchung eines Systems indem ein Modell aus Sicht der (künftigen) Benutzer beschrieben wird und *Use Cases* definiert werden.
Es ist wichtig, dass keine Implementierungsentscheidungen hier getroffen werden.

*Datenanalyse*
Systematische Auswertung umfangreicher Informationssammlungen, die neu erstellt werden oder bereits vorliegen.

*Prozessanalyse*
Es werden die Abläufe von Prozessen untersucht, mit dem Ziel diese zu optimieren.

## Entwurf
Nach der Analyse wird ein *Entwurf* des Systems angefertigt, der als Implementierungsvorlage dient und die einzusetzenden Technologien (Hardware, Programmiersprache, Betriebssysteme, etc.) festlegt sollte dies noch nicht erfolgt sein.

>[!note]
>Extreme Programming und Agile verzichten auf einen Entwurf.

Der Entwurf beschreibt die *Architektur* eines Produkts, also den Aufbau und das Zusammenwirken der einzelnen Komponenten. 
Zur Erstellung werden die folgenden Fragen gestellt:
- Welche Elemente gehören zum System und welche sind außerhalb?
- Über welche Schnittstellen kommuniziert das System mit seiner Umgebung?
- Über welche Schnittstellen kommunizieren die einzelnen Komponenten miteinander?
- Welche Aufgaben muss das System selbst erfüllen und für welche greift es auf vorhandene Komponenten zurück?
- Wird das System als *Stand-alone-System* (auf einem einzelnen Computer) oder als *verteiltes System* (einzelne Teile kommunizieren über ein Netzwerk) aufgeführt?
>[!note]
>Die [[Server#Zentralisierung|Server-Client-Architektur]] und Peer-to-Peer-Architektur sind Beispiel von verteilten Systemen.

## Implementierung
Bei der *Implementierung* sind folgende Punkte zu beachten:
*Konsistenz*
Festgelegte Konventionen für Bezeichnungen, Schnittstellen, Reihenfolgen, Codestruktur und Kommentare sind immer einzuhalten. Bei Programmierprojekten gehört dazu auch ein *Coding Style*.

*Modularisierung*
Komponenten sollten immer eine Aufgabe erfüllen und mit anderen zusammenarbeiten, das verbessert die Wiederverwendbarkeit von z.B. Code und ermöglicht eine bessere Überschaubarkeit.

*Versionsverwaltung*
Alle Änderungen