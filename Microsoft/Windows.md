# Dateisystem
Im Windows [[Betriebssysteme#Dateisysteme|Dateisystem]] hat jeder Datenträger und Partition einen eigenen Verzeichnisbaum. Die Partitionen werden durch Buchstaben in einer automatisch gewählten Reihenfolge benannt:
- *A*: das erste Diskettenlaufwerk
- *B*: das zweite Diskettenlaufwerk
- *C*: die erste Partition auf der ersten Festplatte 
- *D*: die erste Partition auf der zweiten Festplatte

Dies wird für alle Partitionen und Festplatten weitergeführt, anschließend werden CD-ROM und DVD-Laufwerke zugewiesen. Netzwerkressourcen können als virtuelle Laufwerke mit frei wählbaren Buchstaben eingebunden werden.

# Terminal / CMD

> [!NOTE]
> Über die *Windows Terminal* App hat man die Wahl zwischen:
> - Command Prompt (Cmd)
> - [[PowerShell]]
> - Azure Cloud Shell

- `>Dateiname`
  Die Ausgabe wird in die angegebene Datei umgeleitet, ihr Inhalt wird dabei überschrieben
- `>>Dateiname`
  Die Ausgabe wird in die angegebene Datei umgeleitet, ihr Inhalt wird nicht überschrieben, sondern die Ausgabe wird an das Ende angehängt
- `<Dateiname`
  Der Inhalt der Datei wird als Eingabe gelesen, statt von der Tastatur
- `Befehl1 | Befehl2`
  *Pipe*, leitet die Ausgabe von `Befehl1` als Eingabe an `Befehl2` weiter 

Zur Mustererkennung wird `*` benutzt für beliebig viele beliebige Zeichen und `?` für genau ein beliebiges Zeichen. Um z.B. alle Dateien anzusprechen wird `*.*` benutzt.
Dateien werden als Erstes im aktuellen Arbeitsverzeichnis gesucht und anschließend in den Verzeichnissen die in der Umgebungsvariable `PATH` angegeben sind.

>[!note]
>Die `PATH` Variable kann unter "Umgebungsvariablen" bearbeitet werden, dabei wird zwischen *Systemvariablen*, gelten unabhängig vom angemeldeten User-Account für das gesamte System, und *Benutzervariablen*, gelten nur für den aktuellen Account.

## Befehle
- `dir`
  listet den Inhalt des aktuellen Verzeichnisses auf
	- die Option `/P`  zeigt den Inhalt seitenweise an
	- `/w` lässt ausführliche Informationen weg und verwendet mehrere Spalten für Dateien
	- `/s` gibt zusätzlich die Inhalte aller verschachtelten Unterverzeichnissen an
- `cd`
  wechselt das Verzeichnis, für ein Unterverzeichnis wird der Name angegeben, um in das übergeordnete Verzeichnis zu kommen wird `..` angegeben
- `mkdir Verzeichnisname`
  legt ein neues Verzeichnis an
- `del Datei`
  löscht die angegebene Datei
  es kann auch ein Muster angegeben werden, z.B. `*.txt` angegeben werden und damit werden alle Dateien nach dem Muster gelöscht, zusätzlich kann mit `/s` alle Unterverzeichnisse und deren Inhalte gelöscht werden
- `rmdir Verzeichnis`
  löscht das Verzeichnis, um ein Verzeichnis mit Inhalt zu löschen muss `/s` angegeben werden
- `copy quelle ziel`
  Kopiert eine Datei oder mehrere, in Form von einem Muster, das Ziel muss ein nichtexistierender Name sein
- `move Quelle Ziel`
  verschiebt eine oder mehrere Dateien in ein Verzeichnis
- `rename alterName neuerName`
  Bennent eine Datei um
- `attrib`
  Ändert die Dateiattribute; `+` oder `-` um Attribute an- bzw. auszuschalten; mit `/s` werden auch Unterverzeichnisse angepasst
	- `R`: read-only
	- `S`: Systemdatei
	- `H`: Hidden
	- `A`: Archiv 
- `type`
  zeigt den Inhalt einer Textdatei an