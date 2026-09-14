MySQL ist eine weitverbreitet [[Databases#Relationale Datenbanken|relationale Datenbank]].

> [!NOTE]
> [MariaDB](https://mariadb.com/docs/) ist eine verwandte Datenbank, welche wie MySQL von Michael Widenius entwickelt wurde und MySQL sehr ähnlich ist, jedoch mit größerer Open-Source Regelungen.

# Installation und Start
- https://dev.mysql.com/doc/
- https://mariadb.org/documentation/

# SQL-Abfragen
Mit *Queries* (Abfragen) kann man die Inhalte einer Datenbank verändern und abrufen.
## Anlegen einer Datenbank
```SQL
Create Database verein;
Use name;
```
## Anlegen einer Tabelle
```SQL
Create Table Tabellenname
(
Spaltenname1 Datentyp [Spaltenbedingung],
Spaltenname2 Datentyp [Spaltenbedingung],
[Tabellenbedingung,]
...
);

Create Table Mitglieder
(
Mitnr int auto_increment PRIMARY KEY,
Name varchar (30) NOT NULL,
`Alter` int Null default 18,
Strasse varchar (50)
);
```

>[!note]
>Mit `auto_increment` wird eine einmalige Nummer generiert wenn ein neuer Eintrag in table erstellt wird.

### Datentypen
**Ganzzahlen**:
- `TINYINT`:(8 Bit)
- `SMALLINT`: (16 Bit)
- `MEDIUMINT`: (24 Bit)
- `INT`: (32 Bit)
- `BIGINT`: (64 Bit)

**Fließkommazahlen**
- `FLOAT`: (4 Byte)
- `DOUBLE`: (8 Byte)

**Datum und Uhrzeiten**
- `DATE`: im Format year-month-day
- `TIME`: im Format hour:minute:seconds
- `DATETIME`: im format year-month-day hour:minute:seconds
- `YEAR`:
- `TIMESTAMP`: wird beim Erstellen oder Ändern eines Datensatzes automatisch gestellt

**Textdatentyp**
- `CHAR(n)`: Zeichenkette mit max. Länge n (max. 255 Zeichen)
- `VARCHAR(n)`: Zeichenkette mit max. Länge n (max 65.535 Zeichen)
- `TINYTEXT`: Synonym für `VARCHAR(255)`
- `TEXT`: Text mit max. 65.553 Zeichen
- `MEDIUMTEXT`: Text mit max. 16,7 Millionen Zeichen
- `LONGTEXT`: Text mit max. 4 Milliarden Zeichen

**Binärdaten**
- `TINYBLOB`: max. 255 Byte
- `BLOB`: max. 65.535 Byte
- `MEDIUMBLOB`: max. 16,7 Millionen Byte
- `LONGBLOB`: max. 4 Milliarden Byte

**Aufzählung**
- `ENUM`: Aufzählungen von max. 65.535 verschiedenen Zeichenketten
- `SET`: Aufzählung von max. 65.535 verschiedenen Zeichenketten, die Werte der Felder können aus beliebig viele kommagetrennte Werte aus der Auszählung bestehen 
### Spaltenbedingungen
- [NOT NULL](https://www.w3schools.com/MySQL/mysql_notnull.asp) - Ensures that a column cannot have a NULL value
- [UNIQUE](https://www.w3schools.com/MySQL/mysql_unique.asp) - Ensures that all values in a column are different
- [PRIMARY KEY](https://www.w3schools.com/MySQL/mysql_primarykey.asp) - A combination of a `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table
- [FOREIGN KEY](https://www.w3schools.com/MySQL/mysql_foreignkey.asp) - Prevents actions that would destroy links between tables
- [CHECK](https://www.w3schools.com/MySQL/mysql_check.asp) - Ensures that the values in a column satisfies a specific condition
- [DEFAULT](https://www.w3schools.com/MySQL/mysql_default.asp) - Sets a default value for a column if no value is specified
- [CREATE INDEX](https://www.w3schools.com/MySQL/mysql_create_index.asp) - Used to create and retrieve data from the database very quickly
## Datenbanken verändern
**INSERT**
Neue Datensätze können mit `INSERT INTO`-Statement einer Tabelle hinzugefügt werden.
1. *Hinzufügen eines vollständigen Datensatzes*
   ```SQL
   INSERT INTO tabellenname
   VALUES (wert1, wert2, wert3, ...);
   ```
   >[!caution]
   >Die Anzahl und Reihenfolge der angegebenen Werte muss den Attributen der Tabelle entsprechen.

2. *Hinzufügen eines spezifischen Wertes*
   ```SQL
   INSERT INTO tabllenname (attribut1, attribut2, ...)
   VALUES (wert1, wert2, ...);
   ```

**UPDATE**
Um einzelne Werte von Datensätzen zu überschreiben wird das `UPDATE`-Statement benutzt.
```SQL
UPDATE tabellenname
SET attribut1 = wert1, attribut2 = wert2, ...
WHERE bedingung;
```

**DELETE**
Um einen oder mehrere Datensätze zu löschen wird das `DELETE`-Statement benutzt.
```SQL
DELETE FROM tabellenname
WHERE bedingung;
```

**CHANGE**
Um die Eigenschaften einer Tabelle nachträglich zu ändern, wird der Befehl `CHANGE` benutzt.
```SQL
CHANGE COLUMN aktuellerName neuerName Datentyp [Optionen]

# Name erlaubt nun Namen mit bis zu 50 Zeichen länge
ALTER TABLE Mitglieder
CHANGE COLUMN Name Name VARCHAR(50);
```

**ADD**
Um eine Spalte hinzuzufügen wird `ADD` benutzt.
Standardmäßig wird die neue Spalte am Ende eingefügt, mit `FIRST` oder `AFTER COLUMN spaltenName` kann man die an den Anfang oder nach einer bestimmten Spalte einfügen.
```SQL
ADD COLUMN spaltenName datenTyp [Bedingung]

ALTER TABLE Mitglieder
ADD COLUMN Wohnort VARCHAR(50);
```

**DROP**
Der Befehl `DROP` kann benutzt werden um eine Spalte, eine Tabelle und die gesamte Datenbank zu löschen.
```SQL
DROP COLUMN spaltenName
DROP TABLE tabellenName
DROP DATABASE

ALTER TABLE Mitglieder
DROP COLUMN Strasse;

DROP TABLE Mitglieder;

DROP DATABASE verein;
```
## Datenabfragen

>[!attention] Reihenfolge der Abfrage
>Es wird erst die FROM-, dann die WHERE- und zuletzt die SELECT-Klausel ausgewertet.

>[!attention] Syntax Reihenfolge
>```mysql
>SELECT column-name(s)  
>FROM table_name  
>WHERE condition  
>GROUP BY column_name(s)  
>HAVING condition  
>ORDER BY column_name(s)
>```
### Abrufen von Daten mit Select
Die Syntax einer SQL Abfrage hat folgende Elemente:
- *Select*: Liste der auszugebenden Attribute
- *From*: Liste der Tabellen, aus denen Daten entnommen werden
- *Where*: Bedingungen, die die Datensätze erfüllen müssen
- *Order by*: Attribute, nach denen sortiert werden soll

>[!tip]
>Um Alle Attribute auszugeben kann man `SELECT *` angeben.

**Aggregatfunktionen**
Aggregatfunktionen führen Berechnungen über eine Menge von Werten durchführen und ein einzelnes Ergebnis zurückgeben.
Die wichtigsten Aggregatfunktionen sind:
 -  *MIN()*: gibt den kleinsten Wert einer Spalte zurück 
 -  *MAX()*: gibt den größten Wert einer Spalte zurück 
 - *COUNT()*: zählt die Anzahl der Zeilen in einer Gruppe 
 - *SUM()*: berechnet die Summe aller Werte in einer numerischen Spalte 
 - *AVG()*: berechnet den Durchschnittswert einer numerischen Spalte

>[!note]
>Aggregatfunktionen ignorieren NULL-Werte, mit Ausnahme von COUNT(), das alle Zeilen zählt – auch solche mit NULL

 **Beispiele**
1. Jahresgehälter aller Mitarbeiter sollen ausgegeben werden
   ```sql
   SELECT Persnr, Nachname, 12*Gehalt
   AS Jahresgehalt
   FROM Mitarbeiter
   ```
2. Gesamte Personalkosten pro Jahr sollen ermittelt werden
   ```sql
   SELECT 12*SUM(Gehalt)
   AS Personalkosten
   FROM Mitarbeiter
   ```
3. Anzahl der Mitarbeiter
   ```sql
   SELECT COUNT(*)
   FROM Mitarbeiter
   ```

>[!note] 
>Mit `AS` kann man die Spaltenüberschrift bei der Ausgabe ändern.

**Distinct**
Mit `SELECT DISTINCT` werden nur unterschiedliche Werte ausgegeben

**Beispiel**
Es sollen die Herkunftsländer von Kunden ausgewertet werden:
```sql
SELECT Country
FROM Costumers
```
Dies ergibt die folgende Ausgabe:

| Country |
| ------- |
| Germany |
| Mexico  |
| Mexico  |
| UK      |
| Sweden  |
| Germany |
Mit `distinct`:
```sql
SELECT DISTINCT Country
FROM Country
```
Dies ergibt folgende Ausgabe:

| Country |
| ------- |
| Germany |
| Mexico  |
| UK      |
| Sweden  |

---
Es sollen die Arbeiter und ihre Vorgesetzten ausgegeben werden
```sql
SELECT COUNT (*)
FROM Mitarbeiter
```
-> 9 Ergebnisse 

```sql
SELECT COUNT(Vorgesetzter)
FROM Mitarbeiter
```
-> 7 Ergebnisse; zählt nicht die Einträge mit `null` Wert bei "Vorgesetzter"

```sql
SELECT COUNT(DISTINCT Vorgesetzter)
FROM Mitarbeiter
```
-> 2 Ergebnisse; zählt nur unterschiedliche Einträge
### Bedingungen mit Where
Die `WHERE`-Anweisung erlaubt die Ausgabe von komplexen Bedingungen:
- Vergleiche: `WHERE GebDat > '1970-12-11`
- Mehrere Bedingungen mit `AND`, `OR` und `NOT`
- Filtern von Text-Attributen mit `LIKE`

>[!warning]
>Der Datentyp eines Attributs muss in der Bedingung beachtet werden:
>- Bei *Text*-Attributen müssen die Werte in einfachen Hochkommata ausgegeben werden, z.B. `Name= 'Lindemann'`
>- Bei *Zahl*-Attributen werden Werte ohne Anführungszeichen geschrieben
>- *Datumsangaben* werden nach amerikanischem Schema geschrieben (Jahr-Monat-Tag) und werden in Anführungszeichen gesetzt, z.B. `GebDat = '1970-06-23'` 

**LIKE-Vergleich**
Beim LIKE-Vergleich können Platzhalter für Texte angegeben werden:
- *%*: beliebig viele Buchstaben
- *_*: ein beliebiger Buchstabe

Es sollen nur diejenigen Mitarbeiter ausgegeben werden, deren Vorname mit einem B beginnt:
   ```sql
   SELECT *
   FROM Mitarbeiter
   WHERE Vorname LIKE 'B%'
   ```
### Operatoren
**Beispiele**
1. Es soll das kleinste Gehalt zurückgeliefert werden, das größer als 3000€ ist:
   ```sql
   SELECT MIN(Gehalt)
   FROM Mitarbeiter
   WHERE Gehalt > 3000
   ```
2. Es sollen alle Mitarbeiter angezeigt werden deren Vorname Bernd lautet:
   ```sql
   SELECT *
   FROM Mitarbeiter
   WHERE Vorname='Bernd'
   ```
3. Es sollen alle Mitarbeiter ausgegeben werden die einschließlich zwischen 2000 und 3000€ im Monat verdienen:
   ```sql
   # Lösung mit Vergleichsoperatoren
   SELECT *
   FROM Mitarbeiter
   WHERE Gehalt>=2000 AND Gehalt<=3000

   # Lösung mit Intervalloperatoren
   SELECT *
   FROM Mitarbeiter
   WHERE Gehalt BETWEEN 2000 AND 3000
   ```

4. Ausgabe aller Mitarbeiter die keinen Vorgesetzten haben:
   ```sql
   SELECT *
   FROM Mitarbeiter
   WHERE Vorgesetzt IS Null
   ```

### Unterabfragen 
Es können zusätzliche Datenabfragen in der `WHERE` Klausel abgefragt werden

**Beispiele**:
1. Ermitteln des Mitarbeiters mit dem höchsten Gehalt
   ```sql
   SELECT *
   FROM Mitarbeiter
   WHERE Gehalt = (SELECT MAX(Gehalt) FROM Mitarbeiter)
   ```
2. Gesucht sind alle Mitarbeiter die weniger als Herr Kruse mit Persnr 8 verdienen:
   ```sql
   SELECT *
   FROM Mitarbeiter
   WHERE Gehalt<(SELECT Gehalt FROM Mitarbeiter WHERE Persnr=8)
   ```
## Sortieren in SQL mit Order BY
Um Datensätze sortiert auszugeben benutzt man die `ORDER BY` Anweisung. 
Zusätzlich gibt es die Schlüsselworte:
- *ASC*: aufsteigende Sortierung (Standard)
- *DESC*: absteigende Sortierung


**Beispiel**:
- Die Daten aller Mitarbeiter sollen sortiert nach Ort, Straße und Hausnummer ausgegeben werden.
  ```sql
  SELECT *
  FROM Mitarbeiter
  Order BY Ort, Strasse, Hausnr 
  ```
- Ermitteln der Anzahl der Mitarbeiter die in einem Ort wohnen. Ausgabe absteigend sortiert nach Anzahl, aufsteigend nach Ort
  ```sql
  SELECT Ort, COUNT(*) AS Anzahl
  FROM Mitarbeiter
  GROUP BY Ort
  ORDER BY COUNT(*) DESC, Ort
  ```
## Group by and Having
- Mit `Group by` können gleiche Abfrageergebnisse gruppiert werden
- Mit `Having` können zusätzliche Aggregatsfunktionen ausgeführt werden

**Beispiel**:
- Ermittle Orte in denen mindestens zwei Mitarbeiter wohnen
  ```sql
  SELECT Ort, Count(*) AS Anzahl
  FROM Mitarbeiter
  GROUP By Ort
  HAVING COUNT(*) > 1
  ```
- Es soll zusätzlich das höchste Gehalt und die Summe der Gehälter der Mitarbeiter ausgegeben werden
  ```sql
  SELECT Ort, COUNT(*) AS Anzahl, MAX(Gehalt) AS Maximum, SUM(Gehalt) AS Summe
  FROM Mitarbeiter
  GROUP BY Ort
  HAVING COUNT(*) > 1
  ```

## Verknüpfung von Tabellen mit join

Here are the different types of the JOINs in SQL:
- *(INNER) JOIN*: Returns records that have matching values in both tables
- *LEFT (OUTER) JOIN*: Returns all records from the left table, and the matched records from the right table
- *RIGHT (OUTER) JOIN*: Returns all records from the right table, and the matched records from the left table
- *FULL (OUTER) JOIN*: Returns all records when there is a match in either left or right table


### (INNER) JOIN
Join is used to combine rows from two or more tables based on a related column between them.

**Example**:

| OrderID | CustomerID | OrderDate  |
| ------- | ---------- | ---------- |
| 10308   | 2          | 1996-09-18 |
| 10309   | 37         | 1996-09-19 |
| 10310   | 77         | 1996-09-20 |
^ "Orders" table

| CustomerID | CustomerName                       | ContactName    | Country |
| ---------- | ---------------------------------- | -------------- | ------- |
| 1          | Alfreds Futterkiste                | Maria Anders   | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Mexico  |
| 3          | Antonio Moreno Taquería            | Antonio Moreno | Mexico  |
^ "Customers" table

If we want to know what customer did what order and what the date is we use join:
```sql
select Orders.OrderID, Customer.CustomerName, Orders.OrderDate
from Orders
join Customer on Orders.CustomerID-Customers.CustomerID
```

This SQL statement will give you the following result:

|OrderID|CustomerName|OrderDate|
|---|---|---|
|10308|Ana Trujillo Emparedados y helados|9/18/1996|
|10365|Antonio Moreno Taquería|11/27/1996|
|10383|Around the Horn|12/16/1996|
|10355|Around the Horn|11/15/1996|
|10278|Berglunds snabbköp|8/12/1996|
### Self Join
Self Join is a regular join, but it joins a table with itself.
**Beispiel**:
- Der Chef will eine nach Namen sortierte Liste der Mitarbeiter. Dabei soll zu jedem Mitarbeiter der Name des Vorgesetzten ausgegeben werden.
  ```sql
  SELECT M.Nachname, M.Vorname, V.Nachname AS NachnameChef, V.Vorname AS VornameChef
  FROM Mitarbeiter M 
  Join Mitarbeiter V ON M.Vorgesetzter = V.Persnr
  ORDER BY M.Nachname, M.Vorname  
  ```
### Outer Join
Outer Join returns all records when there is a match in the left or right table, even if there is no match between the rows.
**Example**:
We want to select all customers and all orders
```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL OUTER JOIN Orders ON Customers.CustomerID=Orders.CustomerID
ORDER BY Customers.CustomerName
```

This will give the following result:

| CustomerName                       | OrderID |
| ---------------------------------- | ------- |
| NULL                               | 10309   |
| NULL                               | 10310   |
| Alfreds Futterkiste                | NULL    |
| Ana Trujillo Emparedados y helados | 10308   |
| Antonio Moreno Taquería            | NULL    |
### Left Join
A Left Join returns all records from the left table and the matching records from the right table
**Example**:
We want to select all customers, and any orders they might have
```sql
SELECT Customers.CustomerName, Orders.OrderID  
FROM Customers  
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID  
ORDER BY Customers.CustomerName
```

This will give the following result:

| CustomerName                       | OrderID |
| ---------------------------------- | ------- |
| Alfreds Futterkiste                |         |
| Ana Trujillo Emparedados y helados | 10308   |
| Antonio Moreno Taquería            | 10383   |
| Around the Horn                    | 10355   |
| Berglunds snabbköp                 | 10278   |
### Right Join
A Right Join returns all records from the right table and the matching records from the left table
**Example**:
We want to select all all employees, and any orders they might have placed:
```sql
SELECT Orders.OrderID, Employees.LastName, Employees.FirstName  
FROM Orders  
RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID  
ORDER BY Orders.OrderID
```

# Transaktionen
Transaktionen ermöglichen es beliebig viele Einzelschritte zusammenzufassen und dann zu bestätigen (Commit) oder rückgängig machen (Rollback). 
Gewünschte Eigenschaften von Transaktionen *ACID*:
- *Atomicity*: 
  Die Transaktion fasst die einzelnen MySQL Anweisungen zu einer einzelnen Anweisung zusammen
- *Consistency*:
  Nach Commit oder Rollback eines Commits muss die Datenbank konsistent sein/bleiben.
- *Isolation*:
  Jede Transaktion muss von anderen Operationen und Transaktionen isoliert sein, d.h. die einzelnen Operationen bemerken nichts von anderen.
-  *Durability*:
  Nach einem Commit müssen die Änderungen dauerhaft in der Datenbank gespeichert sein

Transaktionen werden nur durch den Tabellentypen InnoDB unterstützt, bei Windows ist es der Standardtabellentyp. Bei Linux hingegen ist es MyISAM, da diese performanter ist.

- Erzeugen einer InnoDB Tabelle:
```SQL
CREATE TABLE tabellenName(
...
) ENGINE=InnoDB
```
- **Transaktion starten**
`START TRANSACTION;`
- **Änderungen bestätigen**: 
  `COMMIT;`
- **Änderungen abbrechen**:
  `ROLLBACK;`
- **Änderungen zwischenspeichern**:
  `SAVEPOINT name;`
- **Zurückgehen auf einen Savepoint**
  `ROLLBACK TO nameSavepoint;`

