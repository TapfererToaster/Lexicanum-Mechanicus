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
Alle Änderungen am Code sollten dokumentiert werden, dadurch können Auswirkungen auf andere Programmteile bessererkannt und Änderungen auch wieder rückgängig gemacht werden.
Tools zur Versionsverwaltung ist z.B. [[Git]]

## Tests
Bei Softwaretest wird zwischen zwei Arten unterschieden:
- *Whitebox-Tests*: der zu testende Code ist bekannt
- *Blackbox-Tests*: Schnittstellen und Funktionalitätsdefinitionen sind bekannt, der Code selbst ist nicht bekannt

Während der Implementierung sind vier Testarten wichtig:
- *Unit-Tests*:
  automatisierte, programmgesteuerte Test, die die Funktionalität von Klassen und ihren Bestandteilen prüft, für viele Programmiersprachen stehen xUnit-Frameworks (z.B. JUnit) für diese Test zur Verfügung.
- *Integrationstest*:
  Die Zusammenarbeit der verschiedenen Komponenten wird überprüft, diese können auch mithilfe der xUnit-Frameworks durchgeführt werden.
- *Frontend-Tests* / *End-to-End-Tests*:
  Hierbei wird das *Frontend* (Benutzeroberfläche) getestet, diese können Teils auch automatisiert erfolgen (z.B. [Selenium](https://www.selenium.dev/))
- *Schreibtischtest*:
  Der Programmierer erstellt für einen Codeblock, eine Funktion oder Methode eine Tabelle mit der Wertänderungen verschiedener Variablen bei unterschiedlichen Eingabewerten verfolgt werden.
- *Code-Reviews*:
  Im Team überprüft ein Programmierer den Code eines anderen Programmierers

## Dokumentation 
>[!warning]
>Die Dokumentation sollte nicht erst als letztes angefertigt, sondern parallel zum gesamten Ablauf des Projekts werden.

Es gibt bei Dokumentationen mehrere Arten:
- *Entwicklungsdokumentation*:
  Beschreibung von Klassen, Modulen, Schnittstellen und Erweiterungsmöglichkeiten;
  bildet die Grundlage für Änderungen und Erweiterungen
  Beispieltool: [Javadoc](https://de.wikipedia.org/wiki/Javadoc)
- *Administratorendokument*:
  für technisches Fachpersonal vorgesehen und enthält ausführliche Installations- und Konfigurationsanleitungen.
- *Anwendungsdokumentation*:
  Beschreibt den Einsatz, Aufgaben und die Verwendung von Software, vergleichbar mit einer Bedienungsanleitung. Sollte nicht so technisch wie die Administratorendokumentation, sondern in leichter und verständlicher Sprache geschrieben sein. Zusätzlich sollte sie sehr nahe an der Arbeitsweise der Benutzer sein.

# Entwicklungsverfahren
## Unified Process
*Unified Software Development Process* wurde zusammen mit [[UML]] definiert und verwendet es für Darstellungen von Anwendungsfällen, Ablaufen und Entwürfen.

Merkmale des Unified Process sind:
- *Use Cases* (Anwendungsfälle)
  Die Bedürfnisse der Benutzer werden durch Anwendungsfälle dargestellt und in Beziehungen zu Vorgängen und Geschäftsvorfällen gesetzt. Die Software wird dann basierend auf den Use Cases modelliert.
>[!note]
>Statt von Benutzern wird auch von *Akteuren* gesprochen, um auch Geräte oder Programme und nicht nur Menschen einzubeziehen.
- *Architekturzentriert*:
  Es werden anwendungsfallunabhängige Architekturteile modelliert, etwa Schnittstellen zur Zielplattform, diese werden dann mit UML dargestellt und in eine Architektur umgesetzt.
- *Iterativer Prozess*
  Unified Process ist eine iterativer Prozess, der Entwicklungszyklus wird mehrfach durchlaufen und das Produkt schrittweise erweitert und verbessert.

Folgende Begriffe werden im Unified Process verwendet:
- *Rollen*: Wer?
  beschreiben die Aufgaben und Zuständigkeitsbereiche von Gruppen und Mitgliedern
- *Aktivität*: Wie?
  Jede Rolle besteht aus einer Abfolge von Aktivitäten, welche ein bestimmtes (Teil-)ziel erreichen sollen
- *Artefakte*: Was?
  Artefakte sind die durch Aktivitäten erarbeiteten Projektteile; der Startpunkt eines Verarbeitungsschritt nennt man *Eingangsartefakt*, der Abschluss *Endartefakt*.
- *Vorgehen*: Wann?
  Ein Vorgehensmodell beschreibt die zeitliche Abfolge von Aktivitäten

Die einzelnen Phasen des Unified Process sind:
1. **Konzeptionsphase**:
   - Anwendungsfälle werden gesammelt, geordnet und ausgewertet
   - Vorentscheidungen über den Projektfokus und -umfang werden getätigt
   - Der Entwurf der Architektur wird begonnen
2. **Entwurfsphase**:
   - Der Architekturentwurf wird fertig gestellt
   - Kernkomponenten werden implementiert
   - Teilergebnisse werden besprochen und ggf. korrigiert
   - Test und Dokumentation werden begonnen
3. **Konstruktionsphase**:
   - Alle Teile des Systems werden fertig implementiert, getestet und dokumentiert
   - Die einzelnen Bestandteile werden zu einem Gesamtsystem zusammengefügt
4. **Übergangsphase**:
   - Das System wird zu einem veröffentlichungsfähigen Paket zusammengestellt
   - Das Paket wird beim Kunden installiert und die Benutzer eingewiesen / geschult

## Extreme Programming
*Extreme Programming (XP)* konzentriert sich stark auf die Programmierung, während Planung, Analyse und Entwurf kurz gefasst werden.

>[!note]
>XP gehört zu den *agilen* Entwicklungsmethoden, bei diesen gibt es nur wenige feste Vorgaben und Änderungen der Anforderungen ind Vorgaben können jeder Zeit umgesetzt werden.
>

Merkmale des Extreme Programming:
- *Kurze Release-Zyklen*:
  Bei XP werden Iterationsziele definiert, die in wenigen Tagen oder Wochen erreichbar sind.
- *Häufige Integration*:
  Durch die kurzen Release-Zyklen müssen die einzelnen Komponenten häufiger zu einem Gesamtsystem zusammengefügt werden.
- *Einbeziehung der Kundschaft*:
  Jeder einzelne Entwicklungsschritt wird mit der Kundschaft besprochen und das weitere Vorgehen wird mit ihnen abgestimmt.
- *Programmierung in Paaren*:
  Beim Programmieren sitzen zwei Programmierer vor einer Aufgabe, wobei beide Überlegungen anstellen jedoch nur einer tippt. Bei jeder Aufgabe sollten die Paare wechseln und Code-Reviews integriert werden.
- *Test-first-Verfahren*:
  Es wird immer ein Unit-Test ausgeführt, nur wenn dieser scheitert wird neuer Code hinzugefügt oder geändert.
- *Integriertes Refactoring*:
  Durch das Test-first-Verfahren und die häufigen Releases wird der Code fast automatisch regelmäßig aufgeräumt und an neue Gegebenheiten angepasst.

## Scrum
Bei *Scrum* (Gedränge) wird weitestgehend auf die Selbstorganisation des Teams gesetzt.
>[!note]
>Scrum gehört zu den agilen Entwicklungsmethoden.

Beim Scrum gibt es folgende Rollen:
- *Product Owner*:
  Ist für das Projektmanagement, Organisation von Team-Meetings, sowie die Vorgabe der Projektziele und die Verantwortung gegenüber der Kundschaft, verantwortlich.
- *Team*:
  Besteht aus 5 bis 9 Mitgliedern; setzten die Anforderungen des Projekts durch, wobei jedes Teammitglied, in Absprache mit den anderen, selbst über seine Aufgaben bestimmt.
- *Scum Master*:
  Überwacht die Produktivität des Teams und klärt Probleme.