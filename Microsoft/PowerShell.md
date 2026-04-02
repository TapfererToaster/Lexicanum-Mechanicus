
Die PowerShell ist eine von Microsoft entwickelte Shell und kann auch auf Linux und macOS benutzt werden. 
Sie basiert auf der .NET-Bibliothek und erlaubt objektorientierten Zugriff auf Dateien, Verzeichnisse und andere Elemente; des Weiteren besitzt sie Programmierfeatures wie Variablen und Kontrollstrukturen. 

Für Aktionen werden *Commandlets (Cmdlets)* benutzt. Diese haben neben dem eigentlichen Namen, wie z.B. `Get-ChildItem`, kürzere Aliase, wie z.B. `ls` und `dir`.

# Ausdrücke, Operationen und Variablen
PowerShell kann arithmetische Funktionen auswerten.
```Powershell
> 2 * 3 + 4 - 5 / 6
> 9,16666666666667
```

Der `*`  und `+` Operator kann auch benutzt werden um Strings zu vervielfältigen
```Powershell
> "ha" * 3
> hahaha
> "Test " + 3 + 4
> Test 34
```

## Vergleichsoperatoren
