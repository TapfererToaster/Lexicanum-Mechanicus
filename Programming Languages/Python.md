- https://docs.python.org/3/tutorial/
- http://getpython3.com/diveintopython3/index.html
- https://scapy.readthedocs.io/en/latest/introduction.html

Python ist eine Multiparadigmen Sprache, hat also Aspekte einer imperativen, objektorientierten und funktionalen Programmiersprache.
Der Quellcode wird während der Laufzeit des Programmes vom *Python-Interpreter* übersetzt. Kompiliert wird der Code durch einen *Just-in-Time* Compiler, bei dem der Code nicht Zeile für Zeile während der Ausführung übersetzt wird, sondern viel schneller und übersetzt im Arbeitsspeicher oder auf einem Datenträger zwischengespeichert.

>[!note]
>Auf den meisten [[Linux]] Distributionen ist Python vorinstalliert und man kann mit `python3 datei_name` auf der Konsole Programme ausführen. 
>Mit `python3` wird auf der Konsole ein Interpreter gestartet 

# Syntax
In Python werden Anweisungen nicht mit einem Semikolon beendet, sondern mit einem Zeilenumbruch.
Semikolons können benutzt werden um mehrere Anweisungen in eine Zeile zu schreiben.
```python
print("Hallo"); print("Welt")
```

Um eine Anweisung über mehrere Zeilen zu schreiben benutzt man einen Backslash `\` am Ende der Zeile oder man benutzt Klammern.
```python
2 * 3 * 4

2 * \
3 \
* 4
  
(2 *
3
* 4)
```

Um die Zusammengehörigkeit von Code zu signalisieren werden Einrückungen (von 4 Leerzeichen) benutzt.
```python
if Amweisung:
	print("...")
```

Einzeilige Kommentare werden durch Angabe einer Raute `#` eingeleitet, mehrzeilige mit drei doppelten Anführungszeichen `"""`
```python
# Das ist ein Kommentar

""" Das ist 
ein Kommentar 
über mehrere Zeilen """
```


# Datatypes
![[Python Datatypes.png]]

> [!NOTE] Literals
> Literale sind die einfachste Form von Ausdrücken. Ints, Floats und Strings gehören dazu.
## Integers
Integer haben nicht wie in anderen Programmiersprachen einen feste Speichergröße, 32 oder 64 bit, sondern können beliebig große Zahlen darstellen.
Integer können auch als Binär-, Oktal oder Hexadezimalzahlen geschrieben werden.
```python
0b101010 # Binär   

0x2A # Hexadezimal

0o52 # Oktal
```

Man kann auch Integer in verschiedene Zahlensysteme umwandeln
```python
# Dezimal -> Binär
bin(42)

# Hexadezimal -> Oktal
oct(0x2A) 
```

## Floating Point Numbers
Diese Literale werden mit einem Dezimalpunkt geschrieben, z.B. `0.3` oder mit Exponentialschreibweise, z.b. `4e4` für $4*10^4$. 
Floats haben eine feste Speichergröße von 64 bit.

>[!note]
>Bei Python gehören Komplexe Zahlen zur Grundausstattung und sind direkt unterstützt.
>```python
>complex(Realteil, Imaginärteil)
>```
>Mit `.real` und `.imag` kann der Real- oder Imaginärteil geliefert werden.

## Strings
Strings können mit doppelten `""` oder einfachen `''` Anführungszeichen geschrieben werden.

- **Definition**:
	```python
string1 = "Hello"
string2 = "World"
	```
- **Concatenate Strings**:
  ```python
  print("The message is:" + string1 + string2)
  ```
- **Multiply Strings**
  ```python
  print("Ho! "* 3)
  ```

### Strings formatieren
Syntax
```python
String.format(Wert1, Wert2)
```

Der String enthält `{}` als Platzhalter für die Werte die nach dem String angegeben werden
```python
print("{} {}".format("Hello", "world")
```

Man kann mit Angabe eines Index auch die Reihenfolge der Argumente bestimmen
```python
print("It is a {1}, {1} {0} world".format("world","mad"))
```

Die Platzhalter können auch mit Parametern gefüllt werden.
```python
print("{dividend} / {divisor} = {quotient}".format(dividend = 20, divisor = 5, quotient = 20//5))
```

Eine neuere Möglichkeit der Stringformatierung ist die Verwendung von eingebetteten Ausdrücken
```python
text = "World"
print(f"Hello {text}")
```
### Using built-in methods of strings
- **upper() and lower()**
  helpful when comparing strings that do not need to be case-sensitive; will return the string in all upper or lower case letters
  ```python
  >>>text = 'Test'
  >>>text.lower()
  'test'
  >>>text.upper()
  'TEST'
  ```
  the original variable will not be altered
- **startswith() and endswith()**
  these methods are used to verify if a string starts or ends with a certain sequence of characters
  ```python
  >>> ipaddr = '10.100.20.5'
  >>> ipaddr.startswith('10')
  True
  >>>ipaddr.startswith('100')
  False
  >>>ipaddr.endswith('.5')
  True
  ```
- **strip()**
  this method returns objects without any spaces at the beginning and end
  ```python
  >>>ipaddr = '  10.100.20.5   '
  >>>ipaddr.strip()
  '10.100.20.5'
  ```
- **isdigit()**
  this method checks if a string consists of digits and returns True or False
  ```python
  >>>ten = '10'
  >>>ten.isdigit()
  True
  >>>bogus= '10a'
  >>>bogus.isdigit()
  False
  ```
- **count()**
  allows you to count the number of single characters or character sequences
  ```python
  >>>octet= '11111000'
  >>>octet.count('1')
  5
  >>>octet.count('111')
  1
  >>>test_string= "What would you wish for if you had three wishes"
  >>>test_string.count('you')
  2
  ```
- **format()**
  used to format the output strings 
  ```python
  >>>ping= 'ping {} verf {}'.format(ipaddr,vrf)
  >>>print(ping)
  ping 8.8.8.8 vrf management
  ```
- **join() and split()**

## List
Listen sind indexorientierte Sammlungen beliebig vieler verschiedener Elemente
```python
liste=[1,2,3, "vier", "fünf"]
```

Der Zugriff auf die einzelnen Listenelemente erfolgt durch den *Indexoperator*. Mit negativen Indexwerten kann man vom Ende der Liste zugreifen.
```python
liste[0]
>>> 1
liste[-1]
>>> "fünf"
liste[3]
>>> "vier"
```

Der Indexoperator kann auch benutzt werden um Elementen neue Werte zuzuweisen
```python
liste[0] = "eins"
```

Werte können mit `.append()` an das Ende einer Liste hinzugefügt werden
```python
liste.append(6)
```

>[!note]
>Um eine leere Liste zu erzeugen
>```python
>liste=[]
>```
### Slices
Man kann aus einer Liste auch ein *Slice*, eine Teilliste, mithilfe des *Slice-Operator*.
Die Syntax ist `[StartIndex:EndIndex:Intervall]`
```python
liste[1:3]
>>> 2,3
```

Wird der Start- oder Endindex weggelassen wird die Liste von Anfang bzw. bis zum Ende ausgewählt
```python
liste[:4]
>>> 1,2,3,"vier"
liste[2:]
>>> 3,"vier","fünf"
```

## Tupel
Tupel ist ein Datentyp mit mehreren unveränderlicher Elementen mit fester Anzahl
```python
tuple = (1,2,3,4,5)
```

Es kann auch über einen Indexoperator und per Sliceoperator auf die Elemente zugegriffen werden.
```python
tuple[1]
>>> 2
tuple[:4]
>>> 1,2,3,4
```

## Set
Ein Set ist eine ungeordnete Sammlung von Elementen, d.h. man kann nicht mit einem Indexoperator auf diese zugreifen.
Ein Set wird als kommaseparierte Liste von Werten in geschweiften Klammern geschrieben.
```python
primzahlen = {2, 3, 5, 7, 13, 17, 19}
```

>[!note]
>Duplikate bei der Wert Zuweisung werden nicht übernommen sondern kommen nur einmal vor
>```python
>set = {1,1,2,2,3,4}
>>>> {1,2,3,4}
>``` 

Da nicht über einen Indexoperator auf die Elemente zugegriffen werden kann, wird der Elementoperator `in` verwendet.
```python
11 in primes
>>> True
```

Um eine leere Liste zu erzeugen wird `set()` benutzt, da `{}` das Zeichen für eine Dictionary ist.

Eine unveränderliche Menge eines sets heißt `frozenset` und wird mit `frozenset()` gebildet.
```python
set1 ={1,2,3}
set2 = frozenset(set1)
```

Es ist möglich die Schnitt-, Vereinigungs- und Differenzmenge eines Sets 
```python
# Differenzmenge
set -= {menge}
# Vereinigungsmenge
set |= {menge}
# Schnittmenge
set &= {menge}
```

## Dictionary
*Dictionaries* sind beliebig lange Listen von Key-Value Paaren, die in geschweiften Klammern stehen und durch einen Doppelpunkt getrennt sind.
```python
weekdays = {"Mo":"Montag", "Di":"Dienstag","Mi":"Mittwoch", "Do":"Donnerstag", "Fr":"Freitag", "Sa":"Samstag","So":"Sonntag"}
```

>[!note]
>Es kann sein, dass die Paare in der Reihenfolge gespeichert werden in der sie angegeben wurden, da nicht die Reihenfolge, sondern die Zuweisung von Schlüsseln zu Werten wichtig ist.

Der Zugriff auf die Werte erfolgt durch Angabe des Keys
```python
weekdays["Sa"]
```

Man kann den Elementoperator `in` oder die `get()` Methode verwenden bevor man einen Zugriff versucht um zu überprüfen ob dieser enthalten ist
```python
"Sa" in weekdays
>>> True
weekdays.get("X")
>>> False
```

Neue Werte können über Angabe eines Keys zugewiesen werden#
```python
dict = {}
dict["banane"] = "gelb"
dict["apfel"] = "rot"
```

# Ein- und Ausgabe
Um Text und Daten auf die Konsole auszugeben wird die Funktion `print()` benutzt.
```python
print("Hallo Welt")
```

Um Eingaben zu lesen wird die Funktion `input()` benutzt.

This function reads data entered by the user and returns that data to the program.
>[!info] Deaf Program
>A program that does not get a user's input is a *deaf program*.

```Python
print("Tell me a secret...")
anything = input()
print("Hmm...", anything, "... That is a good secret.")
```

**Input Function with an Argument**
You can use the `input` function to give a prompt to the user without the `print` function, like above.
```Python
secret = input("Tell me a secret")
print("Hmmm...", secret, "I will not tell anyone.")
```

## Kommandozeilenargumente lesen
Um Argumente einzulesen die bei der Ausführung des Programms in die Kommandozeile eingegeben werden, benutzt man `argv` aus dem `sys` Modul.

# Operatoren

>[!note] Rangordnung der Operatoren
>- Exponent (`**`)
>- Bit-Komplement (~), Plus als Vorzeichen (+) und Minus als Vorzeichen (-)
>- Multiplikation (*), Division (/), ganzzahlige Division (//) und Modulo (%)
>- Addition (+) und Subtraktion (-)
>- Bit-Verschiebung nach links (<<) und nach rechts (>>)
>- bitweises Und (&)
>- bitweises Oder (|) und Exklusiv-Oder (^)
>- kleiner als (<), kleiner oder gleich (<=), größer als (>) und größer oder gleich (>=)
>- gleich (`==`) und ungleich (`!=`)
>- Zuweisungs- und Modifikationsoperatoren (=, +=, -=, *=, /= etc.)
>- Identität (is) und Nichtidentität (is not)
>- Element (in) und Nichtelement (not in)
>- logisches Und (and), logisches Oder (or) und logische Verneinung (not)

## Arithmetische Operatoren

| **Operation**     | **Operator** | **Code**                            |
| ----------------- | ------------ | ----------------------------------- |
| Addition          | `+`          | `summe = summand1 + summand2`       |
| Subtration        | `-`          | `differenz = minunend - subtrahend` |
| Multiplikation    | `*`          | `produkt = faktor1 * faktor2`       |
| Division          | `/`          | `quotient = dividend / divisor`     |
| Ganzzahl Division | `//`         | `quotient = dividend // divisor`    |
| Modulo            | `%`          | `rest = dividend % divisor`         |
| Potenz            | `**`         | `ergebnis = basis ** exponent`      |
>[!note]
>Es gibt neben dem `/` Divisionsoperator auch `//` welcher das Ergebnis als Ganzzahl zurück gibt.

## Bitoperatoren
Mit Bitoperatoren kann man auf die binäre Darstellung von Zahlen zugreifen und Operationen durchführen.
![[Bitoperatoren.png|554x116]]
![[Bitoperatoren 2.png.png]]

## Relationale Operatoren

| **Operator** | **Code**         | **Wahr, wenn**                 |
| ------------ | ---------------- | ------------------------------ |
| `>`          | `zahl1 > zahl2`  | zahl1 größer als zahl2         |
| `<`          | `zahl1 < zahl2`  | zahl1 kleiner als zahl2        |
| `>=`         | `zahl1 >= zahl2` | zahl1 größer oder gleich zahl2 |
| `<=`         | `zahl1 <= zahl2` | zahl1 kleiner der gleich zahl2 |
| `==`         | `zahl1 == zahl2` | zahl1 gleich zahl2             |
| `!=`         | `zahl1 != zahl2` | zahl1 ungleich zahl2           |
>[!note]
>Die Vergleichsoperatoren können auch auf Strings, Listen und andere Typen verwendet werden, solange die verglichenen Werte vom selben Typ sind.

## Logische Operatoren

| **Operator** | **Name**        | **Code**                    | **Wahr, wenn**                                  |
| ------------ | --------------- | --------------------------- | ----------------------------------------------- |
| `and`        | Logisches UND   | `condition1 and condition2` | condition1 und condition2 sind wahr             |
| `or`         | Logisches ODER  | `condition1 or conditon2`   | condition1 oder condition2 oder beide sind wahr |
| `not`        | Logisches NICHT | `not condition`             | condition ist falsch                            |
>[!note]
>Die logischen Operatoren unterliegen der *Short-Circuit-Logik*, d.h. sobald klar ist ob das Ergebnis wahr oder falsch ergibt wird die Auswertung gestoppt.
>Bei `and` passiert das sobald ein Operand `false` ist 
>Bei `or` passiert das sobald ein Operand `true` ist

## Zuweisungsoperatoren
Operatoren können in verkürzter Schreibweise angegeben werden:

**Arithmetische Operatoren**

| **Kurzform** | **Normalform** |
| ------------ | -------------- |
| `x += y`     | `x = x + y`    |
| `x -= y`     | `x = x – y`    |
| `x *= y`     | `x = x * y`    |
| `x /= y`     | `x = x / y`    |
| `x %= y`     | `x = x % y`    |
| `x ++`       | `x = x + 1`    |
| `x --`       | `x = x – 1`    |


**Bitoperatoren**

| **Kurzform** | **Normalform** | **Beschreibung**                                                        |
| ------------ | -------------- | ----------------------------------------------------------------------- |
| `x &= 4`     | `x = x & 4`    | x wird mit der Zahl 4 bitweise-UND verknüpft und x zugewiesen           |
| x \|= 6      | x = x \| 6     | x wird mit der Zahl 6 bitweise-ODER verknüpft und x zugewiesen.         |
| `x ^= 5`     | `x = x ^ 5`    | x wird mit der Zahl 5 bitweise-EXCLUSIV-ODER verknüpft und x zugewiesen |
| `x <<= 1`    | `x = x << 1`   | Bitweises Linksschieben von x um eine Stelle und x zuweisen             |
| `x >>= 1`    | `x = x >> 1`   | Bitweises Rechtsschieben von x um eine Stelle und x zuweisen            |

## Identitätsoperator
Der Identitätsoperator `is` gibt `true` zurück wenn das selbe Objekt referenziert wird.
```python
var1 = [1,2,3]
var2 = var1
var1 is var2
>>> true

[1,2,3] is [1,2,3]
>>> false
```

## Elementoperator
Der Elementoperator `in` gibt true zurück, wenn der linke Operand im rechten enthalten ist.
```python
"al" in "Hallo"
>>> true
```

# Kontrollstrukturen
## If-Verzweigung
Die Syntax für eine If-Verzweigung ist
```python
if Bedingung:
	Anweisung
elif Bedingung2:
	Anweisung2
else:
	Anweisung3
```

Ohne `elif` Anweisung kann die If-Verzweigung als *Conditional Expression* geschrieben werden:
```python
Dann-Wert if Bedingung else Sonst-Wert

a = 5
"Ja,5" if a == 5 else "Nein, keine 5"
```

Diese Ausdrücke können auch einer Variable zugewiesen werden
```python
uhrzeit = 7
var = ("Aufwachen" if uhrzeit == 7 else "Weiterschlafen") 
```

## Match-Case Verzweigung
Bei einer Match-Case Verzweigung wird eine Variable mit mehreren möglichen Werten verglichen und unterschiedliche Anweisungen auszuführen.
```python
match var:
	case wert:
		Anweisung
	case wert2:
		Anweisung2
	case _:
		Anweisung3
```

Der Fall `_` steht für alle nicht definierten Werte und wird oft benutzt um Fehler und ungültige Werte abzufangen.

# Schleifen

Mit den Anweisungen `continue` wird ein Schleifendurchlauf übersprungen und der nächste wird sofort ausgeführt.
Mit `break` wird die gesamte Schleife abgebrochen.
```python
for i in
```
## While-Schleife
```python
while Bedingnung:
	Anweisung
```

Eine Besonderheit von Python ist, dass `while` Schleifen einen `else` Block haben können, dieser wird ausgeführt wenn die geprüfte Bedingung von Anfang an `False` ist. 
```python
x = 12
while x < 10:
	print(x + " ist kleiner als 10")
	x += 1
else:
	print("x war nie kleiner als 10")
```

## For-Schleife
```python
for Variable in Aufzählung:
	Anweisung
```

Um durch eine Reihe von Zahlen zu iterieren wird `range()` benutzt
```python
for i in range(anfangsWert,endWert, Intervall):
	Anweisung
	
for i in range(1,10):
	print(i)
```

Diese Schleifen können benutzt werden um mit dem Elementoperator über Inhalte zu iterieren
```python
snacks = [
	"chips",
	"pretzels",
	"cheesy poofs",
	"Chef's choclate salty balls"
]
for snack in snacks:
	print("Get your " + snack " while supplies last!")
```

For-Schleifen können in eckigen Klammern als *List-Comprehensions* um Listen zu erzeugen
```python
numbers = list(range(1,6))
squares = [numbers ** 2 for number in numbers]
```

Zusätzlich kann dieser Ausdruck mit `if` benutzt werden um Listen zu filtern
```python
gefilterte_liste = [ausdruck for element in liste if bedingung]

evenNumbers = [number for number in numbers if number % 2 == 0]
>>> [2,4]
```
# Fehler und Ausnahmen
Bei Fehlern werden *Exceptions* ausgelöst und führen zu einem Programmabsturz, wenn sie nicht abgefangen werden.
Zum abfangen wird `try-except` benutzt
```python
try:
	Anweisung
except Errortype:
	Anweisung bei Fehler
```

Man kann bei der `except` Anweisung auch spezifische Fehlertypen und sogar mehrere Anweisungen angeben:
```python
dividend = 10
divisor = 0
try:
	result = dividend / divisor
except ZeroDivisionError:
	print("Divisor darf nicht null sein")
except: TypeError:
	print("Operanden müssen Zahlen sein")
```

In eigenem Code kann man `raise` benutzen um eigene Ausnahmen und Fehlermeldungen auszulösen
```python
def function(parameter: int):
	if type(parameter) is not int:
		raise TypeError("Argument muss Integer sein")
	Anweisungen
```

Zusätzlich kann man eigene Ausnahmeklassen von vorhandenen ableiten
```python
class OwnTypeError(TypeError):
	pass
	
def function(parameter):
	if Bedingung:
		raise OwnTypeError("Wrong datatype")
		Anweisungen
```
# Mit Dateien arbeiten
Für den Zugriff auf Dateien werden diese mit `open()` geöffnet, dadurch wird ein Objekt erstellt dessen Methoden zum Lesen und Schreiben in der Datei verwendet wird.
```python
varName = open("datei", "mode = x")

# Absoluter Pfad
datei = open("/Users/Name/file.txt", "mode = r")
# relativer Pfad (Datei ist im selben Ordner)
datei = open("file.txt", "mode = w")
```
Der Mode beschreibt was mit der Datei gemacht wird:

| **Mode** | **Description** | **If file does not exist** |
| -------- | --------------- | -------------------------- |
| `r`      | Read only       | FileNotFoundError          |
| `w`      | Write only      | Creates file               |
| `a`      | Append only     | Creates file               |
| `x`      | Create          |                            |
| `r+`     | Read and Write  |                            |
| `w+`     | Write and Read  |                            |
| `a+`     | Append and Read |                            |
 Um den gesamten Inhalt einer Datei zu lesen wird `.read()` benutzt
 ```python
 content = file.read()
 print(content)
 ```

>[!note]
>Die `read()` Funktion benutzt einen *File Cursor* der die aktuelle Position markiert von der aus gelesen wird.
>Mit `seek(position)` kann der Zeiger auf eine andere Position gesetzt werden.
>```python
>file.seek(2)
>```

Das Datei-Objekt stellt für Textdateien einen Iterator bereit, mit dem man die Datei zeilenweise auslesen kann.
```python
for line in file:
	print(line.strip())
```

Um in eine Datei zu schreiben wird der Mode `w` benutzt, wobei jeder vorherige Inhalt der Datei gelöscht wird.
```python
file = open("file","w")
file.write("Das wird in die Datei geschrieben")
```
## Verzeichnisinhalte 
Um Verzeichnisinhalte zu lesen wird `listdir` aus dem `os` Modul benutzt
```python
from os import listdir
for file in listdir("."):
	print(file)
```

Des Weiteren kann man mit `isfile` und `isdir`  überprüfen ob ein Verzeichnisinhalt eine Datei oder ein weiteres Verzeichnis ist.
```python
from os import listdir
from os.path import isfile, isdir
def ls(path):
	for entry in listdir(path):
		is isdir(entry):
			print("d {}".format(entry))
		elif isfile(entry):
			print("f {}".format(entry))
		else:
			print("? {}".format(entry))
```

Mit der Funktion `walk(path)` kann rekursiv ein Verzeichnis ausgelesen werden. Als Rückgabe erhält man ein Tupel mit den relativen Pfadnamen des jeweiligen Verzeichnisses, eine Liste der Unterverzeichnisse und eine Liste der Dateien.
```python
from os import walk
for (dir,subdir,diles) in walk("testdir"):
	print("Dir: {}, subdirectories: {}, files: {}".format(dir, subdir,files))
```
# OOP
## Klasse
Um eine Klasse in Python zu erzeugen benutzt man:
```python
class Name:
	# Konstruktor
	def __init__(self,x,y):
		self.x = x
		self.y = y
	
	# String Darstellung
	def __str__(self):
		return"{x} {y}".format(x = self.x, y = self.y)
		
	# Methode / Funktion definieren
	def funktion(parameter1, parameter2,...):
		Anweisungen

# Hauptprogramm
if __name__ == "__main__":
	# Instanzen der Klasse erzeugen
	instanz = Name("x","y")
	
	# Aufrufen der String Darstellung
	print(instanz)
	
	# Aufrufen einer Funktion
	instanz.funktion(parameter1, parameter2)
	
	Anweisungen
```

>[!warning]
>Anders als in anderen Programmiersprachen gibt es in Python keinen Modifikator für Attribute um diese als `privat` zu setzten und so zu verhindern, dass auf sie von außerhalb der Klasse zugegriffen wird.

> [!NOTE]
> Das Hauptprogramm wird nur ausgeführt wenn das Skript direkt aufgerufen wird, wird es importiert um die Klassenbibliothek zu benutzten wird es nicht ausgeführt.
### Klassenkonstanten 
In Python gibt es keine Konstanten, jedoch ist es Konvention, dass in Großbuchstaben geschriebene Variablen als solche zu behandeln sind.
Die Konstanten werden nach dem Klassennamen, aber vor den Methoden definiert:
```python
class Name:
	CONST1 = x
	CONST2 = y

	def methode(self,...):
		Anweisung
```
### Methoden 
Man kann Parametern Standardwerte zuweisen, wodurch man diesen Parametern beim Aufrufen keine Werte übergeben muss.
```python
def funktion(x,y = standardWert):
	Anweisungen
```

Man kann auch Funktionen schreiben, die eine Liste oder ein Dictionary als Parameter akzeptieren. Dafür wird `*args` für Listen und `**kwargs` für Dictionaries benutzt:
```python
def funktion(*args, **kwargs):
	Anweisungen
```

Wenn eine Methode einen Wert zurückgeben soll wird wie üblich `return` benutzt, man muss auch nicht im Funktionskopf den Typ des Rückgabewerts angeben
```python
def funktion()
	return x
```

**Magic Methods**
Magic Methods werden in bestimmten Kontexten automatisch ausgeführt und können für Klassen extra definiert werden.
- https://realpython.com/python-magic-methods/
- [3. Data model — Python 3.14.4 documentation](https://docs.python.org/3/reference/datamodel.html)

| Operator      | Methode          |
| ------------- | ---------------- |
| `+`           | `__add__()`      |
| `-`           | `__sub__()`      |
| `*`           | `__mul__()`      |
| `/`           | `__truediv__()`  |
| `//`          | `__floordiv__()` |
| `-`           | `__neg__()`      |
| `+=`          | `__iadd__()`     |
| `-=`          | `__isub__()`     |
| `other+self`  | `__radd__()`     |
| `orther-self` | `__rsub__()`     |
| `==`          | `__eq__()`       |
| `!=`          | `__ne__()`       |
| `<`           | `__lt__()`       |
| `<=`          | `__le__()`       |
| `>`           | `__gt__()`       |
| `>=`          | `__ge__()`       |
**Type-Hints**
Um in Python den Datentyp von Parametern oder Rückgabewerten festzulegen werden *Type-Hints* benutzt.
Für Parameter wird der Datentyp nach dem Parameternamen und einem Doppelpunkt geschrieben, für Rückgabewerte wird der Datentyp mit einem Pfeil ans Ende des Methodenkopfes geschrieben.
```python
def funktion(parameter: datentyp) -> DatentypRückgabe:
	Anweisungen
```
## Vererbung
```python
class ChildClass(ParentClass):
	Definition
```

Durch die Vererbung erhalten die Child-Klassen auch die Methoden der Eltern-Klasse; mit `super` können die Methoden der Elternklasse aus der Kind-Klasse aufgerufen werden.
```python
class Child(Parent):
	def function(self):
		super().function()
```

>[!note]
>Der Konstruktor der Elternklasse kann ebenfalls mit `super().__init__()` aufgerufen werden.

In Python ist auch eine Mehfachvererbung (*Multiple Inheritance*) möglich, bei der eine Kind-Klasse von mehreren Eltern-Klassen abgeleitet werden kann
```python
class Child(Parent1,Parent2,...):
	Definition
```
# Lambda-Funktionen
Lambda Funktionen sind anonyme Funktionen, die als Objekte dienen und an Variablen oder Funktionen übergeben werden können und auch als Rückgabewert fungieren können.
```python
lambda arg1, arg2, ...: ausdruck
```
# Module Importieren
Um Skripte zu importieren wird `import` benutzt, nach dem Schema
- `import Modulname`
  importiert alle Klassen des Module unter einem Namensraum
  Der Aufruf der Klassen erfolgt mit `Modulname.Klasse()`
- `import Modulname as EigenerName`
  alle Klassen des Module werden unter dem selbstgewählten `EigenerName` importiert
  Der Aufruf erfolgt mit `EigenerName.Klasse()`
- `from Modulname import *` 
  importiert alle Klassen des Moduls in den Namensraum
  Der Aufruf erfolgt mit `Klasse()`
- `from Modulname import Klassenname1, Klassenname2,...`
  importiert eine oder mehrere Klassen aus dem Modul
## Python Standard Library
- Der Großteil der mathematischen Funktionen befinden sich in dem Modul `math`.
- Das Modul `cmath` stellt die meisten Funktionen auch für komplexe Zahlen bereit
- `sys` stellt Funktionen zur Interaktion mit dem OS und der Shell
- `os` ermöglicht den Zugriff auf die hardwarenäheren Teile des Systems
- `re` ermöglicht das Arbeiten mit [[Reguläre Ausdrücke|regulären Ausdrücken]]
- `datetime` erlaubt die Arbeit mit Uhrzeit und Datum 
# Reguläre Ausdrücke
Man kann mit `re.search(regex, string)` in einem String nach einem Treffer für den [[Reguläre Ausdrücke|regulären Ausdruck]] `regex`.  Sollte ein Treffer gefunden werden wird ein Match-Objekt zurück geliefert, sollte es keinen geben erhält man `None`. 
```python
first_vowel = re.search("[aeiou]", "Hello")
>>> 'e'
```

Mit `span()` wird ein Tupel zurück geliefert das die Anfangsposition und die erste Position nicht mehr zum Treffer gehört.
```python
first_vowel.span()
>>> (1,2)
```

- Mit `re.search()` wird in dem gesamten String nach einem Treffer gesucht
- `re.match()` überprüft nur den Anfang des Strings
- `re.findall()` liefert ein Tupel von mehreren zutreffenden Strings zurück

# Systemnahe Programmierung
Mit dem Befehl `fork()` aus dem `os` Modul kann man in Unix Systemen einen neuen [[Betriebssysteme#Prozessverwaltung|Prozess]] erzeugen, der eine identische Kopie eines ursprünglichen Prozesses erstellt. 
Die Prozesse werden dann eingesetzt um unterschiedliche Aufgaben zu erfüllen, um sie zu unterscheiden gibt `fork()` im ursprünglichen *Parent* Prozess die Prozess ID des *Child* Prozesses zurück und im Child Prozess `0`. 
```python
import os

pid = os.fork()

if pid == 0:
	print("Child process")
else:
	print("Parent process. Child: {}".format(pid))
```