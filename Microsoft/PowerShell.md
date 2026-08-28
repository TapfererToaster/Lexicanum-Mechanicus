
Die PowerShell ist eine von Microsoft entwickelte Shell und kann auch auf Linux und macOS benutzt werden. 
Sie basiert auf der .NET-Bibliothek und erlaubt objektorientierten Zugriff auf Dateien, Verzeichnisse und andere Elemente; des Weiteren besitzt sie Programmierfeatures wie Variablen und Kontrollstrukturen. 

Für Aktionen werden *Commandlets (Cmdlets)* benutzt. Diese haben neben dem eigentlichen Namen, wie z.B. `Get-ChildItem`, kürzere Aliase, wie z.B. `ls` und `dir`.

# Befehle
- `cd`/`chdir`: Verzeichnis wechseln
- `cls`: Bildschirminhalt löschen
- `copy`: Kopieren; z.b. eine Datei
- `date`: Datei anzeigen
- `del`/`erase`: Löschen
- `dir`/`ls`: Verzeichnisinhalt anzeigen
- `echo`: Meldung anzeigen
- `kill`: Prozess beenden
- `md`: Verzeichnis erstellen
- `move`: Verschieben z.B. einer Datei
- `rd`: Verzeichnis löschen
- `sleep`: Prozess wird für x Sekunden angehalten
- `type` / `cat`: Dateiinhalt anzeigen
# Ausdrücke, Operationen und Variablen
Die arithmetischen Operatoren in PowerShell sind:
- `+` | `-`
- `*` | `/`
- `%`
- `..`: Gibt einen Bereich an 
  `1..5` -> 1 2 3 4 5

Arithmetische Operatoren können für Zahlen und Strings verwendet werden.
```Powershell
2 * 3 + 4 - 5 / 6
> 9,16666666666667

"ha" * 3
> hahaha
"Test " + 3 + 4
> Test 34
```
# Cmdlets
Cmdlets sind Funktionen die eine spezifische Aufgabe zuständig sind.

Die Syntax der Cmdlets ist