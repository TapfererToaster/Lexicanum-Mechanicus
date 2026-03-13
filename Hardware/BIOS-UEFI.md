Das *Basic Input / Output System (BIOS)*, sowie das moderne *Enhanced Firmware Interface (EFI)* und das das standardisierte *Unified EFI (UEFI)* ist ein *ROM*-Chip der die *Firmware* enthält und sich auf dem Motherboard befindet.

Auf diesem Chip ist ein Programm in Maschinensprache, das beim Einschalten des Rechners automatisch auf eine bestimmte Adresse im Arbeitsspeicher abgebildet und ausgeführt.
Dieses Programm führt den *Power-on Self Test* durch, um die Funktionalität der Hardware zu überprüfen:
- zuerst wird die Grafikkarte überprüft
- dann RAM
- es wird überprüft ob ein Laufwerk vorhanden ist, von dem ein Betriebssystem geladen werden kann
- Tastatur und Maus werden überprüft 

Sollten größere Probleme auftreten wird eine Abfolge von Signaltönen ausgegeben.
Nach dem erfolgreichen POST wird die Kontrolle über den Rechner an den Datenträger übergeben von dem aus OS gestartet werden soll. Der im *Master Boot Record* des Datenträgers enthaltene *Bootloader* für ein bestimmtes OS oder ein *Bootmanager* für eine Auswahl zwischen mehreren Systemen wird daraufhin gestartet.
# ROM
*Read-only Memory (ROM)* sind Speicher deren Inhalt man nicht oder nicht mit normalen Speicherzugriffen durch das OS ändern kann. Zusätzlich bleibt der Inhalt erhalten, selbst wenn die Stromversorgung zum Speicher beendet wird.
Die verschiedenen Arten von ROM sind:
- *ROM*
Ursprünglicher ROM kann nicht verändert werden und hat einen festverdrahteten Inhalt
- *Programmable ROM (PROM)*
Der Inhalt eines PROMs kann genau einmal programmiert werden.
>[!note]
Im Auslieferzustand sind alle Speicherbits auf 1 gesetzt, eine besonders hohe Spannung verdampft das Metall an den Schaltstellen zu den BIts die 0 werden sollen.
- *Erasable PROM (EPROM)*
Der Inhalt von EPROM kann mit einem speziellen Brenner geändert und durch Ultraviolettlicht gelöscht werden.
- *Electronically (EEPROM)*
Weiterentwicklung von EPROM, der Inhalt kann nun auch elektronisch gelöscht werden
- *Flash-EEPROM*
modernste ROM Art, wird auch *Flash-EPROM* genannt, der Inhalt kann durch Software geändert werden wie bei EEPROM, ist aber günstiger und verbraucht weniger Strom. 
# Konfiguration
Um in das BIOS zu kommen muss direkt nach einschalten des Systems eine bestimmte Taste gedrückt werden, diese Taste ist jedoch bei den Herstellern unterschiedlich.