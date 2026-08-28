- https://docs.python.org/3/tutorial/
- http://getpython3.com/diveintopython3/index.html
- https://scapy.readthedocs.io/en/latest/introduction.html
- https://roadmap.sh/python


Python ist eine Multiparadigmen Sprache, hat also Aspekte einer imperativen, objektorientierten und funktionalen Programmiersprache.
Der Quellcode wird während der Laufzeit des Programmes vom *Python-Interpreter* übersetzt. Kompiliert wird der Code durch einen *Just-in-Time* Compiler, bei dem der Code nicht Zeile für Zeile während der Ausführung übersetzt wird, sondern wird viel schneller übersetzt und im Arbeitsspeicher oder auf einem Datenträger zwischengespeichert.

>[!note]
>Auf den meisten [[Linux]] Distributionen ist Python vorinstalliert und man kann mit `python3 datei_name` auf der Konsole Programme ausführen. 
>Mit `python3` wird auf der Konsole ein Interpreter gestartet 
# Syntax
In Python werden Anweisungen nicht mit einem Semikolon beendet, sondern mit einem Zeilenumbruch.
Semikolons können benutzt werden um mehrere Anweisungen in eine Zeile zu schreiben.
```python
print("Hallo"); print("Welt")
```

**Code über mehrere Zeilen**
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

# Variablen
Variablen werden mit einem `=` Werte zugewiesen, dabei ist die Angabe eines Datentypens nicht erforderlich.
```python
var = 1
text = "Hallo Welt"
```

Die Regeln bei der Vergabe von Variablennamen sind:
- gültige Zeichen sind Buchstaben (A-Z, a-z), Ziffern und Unterstriche `_`
- der Bezeichner darf nicht mit einer Zahl beginnen
- es dürfen keine reservierten Wörter wie `print`, `class` und `import` benutzt werden
# Datatypes
![[Python Datatypes.png]]

> [!NOTE] Literals
> Literale sind die einfachste Form von Ausdrücken. Ints, Floats und Strings gehören dazu.

In Python werden alle Daten als Objekte gespeichert, wovon es grundsätzlich zwei Typen gibt:
- einzelne Objekte: Zahlen, Zeichen
- Gruppen von Objekten (*Iterable Objects*): Strings, Listen, Tuppel, Dictionarys und Sets
## Typenumwandlung
Um Datentypen umzuwandeln können kann man die eingebauten Funktionen benutzen, jedoch muss darauf geachtet werden, dass der Umzuwandelnde Wert für den gezielten Datentyp gültig ist.
- `int()`
- `float()`
- `string()`

```Python
text = string(8.8)
zahl = float(text)
zahl2 = int(zahl)
```
## Typ ermitteln
Um den Datentyp einer Variable herauszufinden benutzt man die Funktion `type()`, welche den Typ (die Klasse) des Objekts herausgibt.

```Python
a = 2
type(a)
```
## Zahlen
>[!tip]
>Man kann einen Unterstrich `_` bei langen Zahlen einsetzen um diese leserlicher zu machen.
>z.B. `100_000_000`
### Integers
*Integer* haben nicht wie in anderen Programmiersprachen einen feste Speichergröße, wie 32 oder 64 bit, sondern können beliebig große Zahlen darstellen und auch in den [[Number Systems|Zahlensystemen]] als Binär-, Oktal oder Hexadezimalzahlen geschrieben werden.
```python
42 # Dezimal

0b101010 # Binär   

0x2A # Hexadezimal

0o52 # Oktal
```

Mit den Funktionen `bin()`, `hex()` und `oct()` können Zahlen in die jeweiligen Zahlensysteme umgerechnet werden.
```python
# z.B. Dezimal -> Binär
bin(42)

# z.B. Hexadezimal -> Oktal
oct(0x2A) 

# z.B. Binär -> Hexadezimal
hex(0b1000)
```
### Floating Point Numbers
Diese Literale werden mit einem Dezimalpunkt geschrieben, z.B. `0.3` oder mit Exponentialschreibweise, z.b. `4e4` für $4*10^4$. 
Floats haben eine feste Speichergröße von 64 bit.

>[!note]
>Python unterstutzt nativ Komplexe Zahlen:
>```python
>complex(Realteil, Imaginärteil)
>```
>Mit `.real` und `.imag` kann der Real- oder Imaginärteil geliefert werden.

**Runden**
Um eine Zahl zu runden wird die Funktion `round(x,y)` benutzt. `x` ist dabei die Zahl und `y` gibt die Anzahl von Nachkommastellen an.
Sollte keine Nachkommastelle angegeben werden wird auf die nächste ganze Zahl gerundet

```Python
x = 12 / 7
r = round(x,3)
```
## Byte
`bytes` sind Objekte mit Werten von 0 bis 255 (ein Byte). Jedes Zeichen kann mit einem Byte gespeichert werden und `byte` Objekte können mit einem Byte Literal erzeugt werden.
```Python
# Datentyp byte
by = b'Hello'
# Umwandlung von String to byte
by = bytes("Hello", "UTF-8")
# Umwandlung von byte zu string
st = by.decode()
```
## Boolean
Boolean Objekte geben den Wahrheitswert von anderen Objekten und Ausdrücken wieder, welcher `True` oder `False` sein kann.

**Wahre Objekte**
- *Zahl != 0*: Zahlen die größer oder kleiner 0 sind
- *nicht leere Sequenz*: String, Tupel, Liste mit Elementen
- *nicht leere Dictionaries oder Mengen*

**Falsche Objekte**
- *Zahl ==  0*
- *leere Sequenz*
- *leere Dictionaries oder Mengen*
- *Konstante None*
- *Objekt der Länge 0*: len(x) == 0
## NoneType
`None` ist das einzige Objekt mit dem Datentyp `NoneType`. 
`None` wird unteranderem von Funktionen zurückgegeben, wenn eine Fehler vorkommt.

## Iterierbare Objekte
Für iterierbare Objekte stehen die folgenden Funktionen zur Verfügung:
- `chr()`: liefert das zugehörige Zeichen zu einer Unicode Zahl  
- `filter(func, x)`: untersucht die Elemente eines iterierbaren Objekts x mit einer Funktion die entweder `True` oder `False` zurück gibt und erzeugt ein neues iterierbares Objekt  
- `map(func,x)`: ruft eine Funktion mehrmals mit verschiedenen Parametern x auf  
- `max()`: liefert den größten Wert oder das Objekt mit der größten Summe  
- `min()`: liefert den kleinsten Wert oder das Objekt mit der kleinsten Summe  
- `ord()`: liefert die zugehörige Unicode Zahl zu einem Zeichen  
- `reversed()`: liefert ein iterierbares Objekt in umgekehrter Reihenfolge zurück
- `sorted()`: liefert ein iterierbares Objekt sortiert zurück
- `zip(x)`: verbindet mehrere iterierbare Elemente und erzeugt mit diesen ein neues

**Sequences**
Sequences are a built-in type, representing an ordered and finite collection of items. 
List, tupel, range, string and binary are sequences.

### Strings
*Strings* sind Zeichenketten und somit Sequenzen von einzelnen Zeichen.
Strings können mit doppelten `""` oder einfachen `''` Anführungszeichen geschrieben werden.
**Definition**:
```python
string1 = "text"
string2 = """Hello
		     World"""
```
 **Concatenate Strings**:
```python
  print("The message is:" + string1 + string2)
```
**Multiply Strings**:
```python
  print("Ho! "* 3)
```
#### Built-in methods
**count()**
  allows you to count the number of single characters or character sequences
  ```python
  octet= '11111000'
  octet.count('1')
  >>> 5
  octet.count('111')
  >>> 1
  test_string= "What would you wish for if you had three wishes"
  test_string.count('you')
  >>> 2
  ```
- **find()**
  Returns the position of character or character sqeuenze
```Python
text = "John Mustermann"
erstePos = text.find('m')
zweitePos = text.find('m', erstpos + 1)
```
- **format()**
  used to format the output strings 
  ```python
  ping= 'ping {} verf {}'.format(ipaddr,vrf)
  print(ping)
  >>> ping 8.8.8.8 vrf management
  ```
- **upper() and lower()**
  helpful when comparing strings that do not need to be case-sensitive; will return the string in all upper or lower case letters
  ```python
  text = 'Test'
  text.lower()
  >>> 'test'
  text.upper()
  >>> 'TEST'
  ```
  the original variable will not be altered
- **partition()**
  separates a sequence and returns the parts as tupels
```Python
text = ("John Mustermann")
text.partition("Mu")
```
- **replace(text, newText)**
  replaces a string with another string
```Python
text = "John Mustermann"
text.replace("John", "James")
```
- **split(splitSign)**
  splits a string into multiple parts, which are stored in a list; spaces are taken as the point to split, but it can also be configured
```Python
text("la li lu le lo")
text.split()

text2("la,li,lu,le,lo")
text2.split(",")
```

- **startswith() and endswith()**
  checks if a string starts or ends with a certain sequence of characters and returns `true` or `false`
  ```python
  ipaddr = '10.100.20.5'
  ipaddr.startswith('10')
  >>> True
  ipaddr.startswith('100')
  >>> False
  ipaddr.endswith('.5')
  >>> True
  ```
- **strip()**
  this method returns objects without any spaces at the beginning and end
  ```python
  ipaddr = '  10.100.20.5   '
  ipaddr.strip()
  >>> '10.100.20.5'
  ipaddr.rstrip()
  >>> ' 10.100.20.5'
  ipaddr.lstrip()
  >>> '10.100.20.5 '
  ```
- **isdigit()**
  this method checks if a string consists of digits and returns True or False
  ```python
  ten = '10'
  ten.isdigit()
  >>> True
  faulty = '10a'
  faulty.isdigit()
  >>> False
  ```

- **join() 

### Lists
Listen sind veränderbare indexorientierte Sequenzen beliebig vieler verschiedener Elemente. 
Listen werden in eckigen Klammern angegeben und die Elemente mit Kommas getrennt.
```python
liste = [x,y,z]

liste=[1,2,3, "vier", "fünf"]
```

Um mehrdimensionale Listen zu erzeugen
```Python
mliste = [[liste1],[liste2]]

liste = [["Paris","Fr", "Frankreich"], ["Berlin","De", "Deutschland"]]
```

Der Zugriff auf die einzelnen Listenelemente erfolgt durch den *Indexoperator*. Mit negativen Indexwerten kann man vom Ende der Liste zugreifen.
```python
liste[0]
>>> 1
liste[-1]
>>> "fünf"
liste[3]
>>> "vier"

# Mehrdimensionale Liste
liste[liste][Element]
>>>liste[0][1]
```

Der Indexoperator kann auch benutzt werden um Elementen neue Werte zuzuweisen
```python
liste[0] = "eins"
```

**Funktionen**
- `.append()`: adds an element at the end of the list
```python
liste.append(6)
```
- `count(val)`: returns the number of an element
```Python
liste.count("Berlin")
```
- `index(val)`: returns the position of an element
```Python
liste.index("Berlin")
```
- `insert(pos, val)`: Inserts a value at the defined position
```Python
liste.insert(2, "Berlin")
```
- `remove(val)`: Removes an element
```Python
liste.remove("Berlin")
```
- `reverse()`: inverts the list
```Python
liste.reverse()
```
- `sort()`: sorts the values of the list, strings are sorted alphabetically 
```Python
liste.sort()
```

>[!note]
>Um eine leere Liste zu erzeugen
>```python
>liste=[]
>```

**Operatoren**
Mit den Operatoren `+` und `*` können Listen zusammengefügt und vervielfacht werden.
```Python
l1 = [1,2,3]
l2 = [4,5,6]
l3 = l1 + l2
```

**List Comprehension**
Mit List Comprehensions kann man einfacher Listen aus anderen Listen erzeugen, indem man die Anweisung in eckigen Klammern einer Variable zuweist.
```Python
xListe = [2,4,6,8,10]

# Liste mit doppeltem Wert 
yListe = [element*2 for element in xListe]
```
#### Slices
Man kann aus einer Sequenz auch ein *Slice*, eine Teilliste, mithilfe des *Slice-Operator* erstellen.
Die Syntax ist `seq[StartIndex:EndIndex:Intervall]`
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

Slices können auch auf Zeichenketten angewendet werden
```Python
name = "John Mustermann"
seq = name[0:4]
print(seq)
seq = name[4:]
print(seq)
```

### Set
Ein Set ist eine ungeordnete Sammlung von Elementen, d.h. man kann nicht mit einem Indexoperator auf diese zugreifen. Des Weiteren können in einem Set jedes Element nur einmal existieren.
Ein Set wird als kommaseparierte Liste von Werten in geschweiften Klammern geschrieben oder mit der Funktion `set()` erzeugt.
```python
set = {val1, val2}
set2 = set(x)

primzahlen = {2, 3, 5, 7, 13, 17, 19}
# Zahlen als liste
primzahlen = set([2,3,5,7,13,17,19])
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

> [!NOTE]
> Um eine leere Liste zu erzeugen wird `set()` benutzt, da `{}` das Zeichen für eine Dictionary ist.

**Funktionen**
- `add()`: Fügt ein Elemente einem Set hinzu
  `set.add(x)`
- `clear()`: Leert ein Set
  `set.clear()`
- `copy()`: Kopiert ein Set
  `set2 = set1.copy()`
- `discard()`: Entfernt ein Element
  `set.discard(x)`

**Operatoren**

>[!note]
>*Teilmenge*: alle Elemente einer Menge m1 sind in einer anderen Menge m2 vorhanden und m1 hat weniger Elemente als m2.
>
>*echte Teilmenge*: alle Elemente von einer Menge m1 sind in einer anderen Menge m2 enthalten, m1 hat jedoch genauso viele Elemente von m2.
>
>*symmetrische Differenzmenge*: Es werden die Elemente ermittelt, die in beiden Mengen vorkommen

- `<`, `>`: überprüft ob ein Set eine echte Teilmenge eines anderen Sets ist:
  `set1 < set2`
- `<=`, `=>` überprüft ob ein Set eine Teilmenge eines anderen Sets ist:
  `set1 <= set2`
- `|`: Vereinigungsmenge zweier Sets
  `set3 = set1 | set2`
- `&`: Schnittmenge zweier Sets
  `set3 = set1 & set2`
- `-`: Differenzmenge zweier Sets
  `set3 = set1 - set2`
- `^`: symmetrische Differenzmenge zweier Sets
  `set3 = set1 ^ set2`

> [!NOTE]
> Es ist möglich die Schnitt-, Vereinigungs- und Differenzmenge eines Sets in verkürzter Schreibweise anzugeben
> ```python
> # Differenzmenge
> set1 -= set2
> # Vereinigungsmenge
> set1 |= set2
> # Schnittmenge
> set1 &= set2
> ```
> 

#### Frozen Set
Eine unveränderliche Menge eines sets heißt `frozenset` und wird mit `frozenset()` gebildet.
```python
fset = frozenset(set)

set1 ={1,2,3}
set2 = frozenset(set1)
```

### Tupel
Tupel ist ein Datentyp mit mehreren unveränderlicher Elementen mit fester Anzahl.
Tupel werden mit runden Klammern erzeugt, jedoch funktioniert es auch ohne Klammern.
```python
tuple = (x, y, z)

tuple = (1,2,3,4,5)
```

Um ein mehrdimensionales Tupel zu erzeugen:
```Python
tuple = ((tuple1), (tuple2))

tuple = (("Paris", "Fr", "3.500.000"), ("Rom", "It", "4.200.000"))
```

**Zugriff**
Es kann auch über einen Indexoperator und per Sliceoperator auf die Elemente zugegriffen werden.
```python
tuple[1]
>>> 2
tuple[:4]
>>> 1,2,3,4
```

**Verpacken und Entpacken**
Da mehrere Werte in einem Tupel gespeichert werden können, ist es auch möglich die Werte auf mehrere Variablen zugewiesen werden können, wobei die Anzahl und Reihenfolge der Werte zu beachten ist. 
Man kann jedoch eine Variable mit einem Stern markieren `*`, *starred Variable*, in dieser werden alle restlichen Werte gespeichert, sollten nicht genug Variablen angegeben worden sein.
```Python
# Verpacken
t = 1,2,3

# Entpacken
x,y,z = t

# Entpacken mit starred Variablen
x, y* = t
```
### Dictionary 
*Dictionaries* sind veränderbare beliebig lange Listen von Key-Value Paaren, die in geschweiften Klammern stehen und durch einen Doppelpunkt getrennt sind, wobei die Keys dabei eindeutig sein müssen. 
```python
dict = {key1:val1, key2:val2}

weekdays = {"Mo":"Montag", "Di":"Dienstag","Mi":"Mittwoch", "Do":"Donnerstag", "Fr":"Freitag", "Sa":"Samstag","So":"Sonntag"}
```

>[!note]
>Es kann sein, dass die Paare in der Reihenfolge gespeichert werden in der sie angegeben wurden, da nicht die Reihenfolge, sondern die Zuweisung von Schlüsseln zu Werten wichtig ist.

**Zugriff**
Der Zugriff auf die Werte erfolgt durch Angabe des Keys in eckigen Klammern.
```python
dict[key]

weekdays["Sa"]
```

**Operationen**
Man kann den Elementoperator `in` , `get()` Methode oder eine `if` Verzweigung verwenden bevor man einen Zugriff versucht um zu überprüfen ob dieser enthalten ist
```python
key in dict
>>> True
dict.get(val)
>>> False
if key in dict:
	Anweisung
```


Neue Werte können über Angabe eines Keys zugewiesen werden
```python
dict[key] = val

dict["apfel"] = "rot"
```

Zum entfernen eines Elements benutzt man:
```Python
del dict[key]

del beeren["Erdbeere"]
```

Man kann Listen mit `update` Dictionaries mit anderen zusammenfügen
```Python
dict1.update(dict2)
```

Dictionaries können verglichen werden, ob die selben Elemente vorhanden sind.
Ein Vergleich der Länge, mit `<` und `>`, ist nicht möglich.
```Python
dict1 == dict2
```

#### Views
Mit den Funktionen `items()`, `keys()` und `values()` können unmittelbar verändernde *Views*, Liste der abgefragten Elemente, eines Dictionaries erzeugt werden.
Durch diese Views kann man mit einer `for` Schleife ausgeben.
```Python
i = dict.items()
k = dict.keys()
v = dict.values()
```
# Ein- und Ausgabe
## Ausgabe
Um Text und Daten auf die Konsole auszugeben wird die Funktion `print()` benutzt.
```python
print("Hallo Welt")
```
### Formatierungen
**Separator und Zeilenende**
Mit dem Separator `sep` und dem Zeilenende `end` kann das Zeichen, das Objekte und Zeilen von einander trennt, geändert werden. Normalerweise ist der Separator ein Leerzeichen und das Zeilenende ein Zeilenumbruch.
```Python
print(x, sep= "separator", end= "end")

print("Stadt", x, sep=":", end="##")
>>> "Stadt:München ## Stadt:Wien ##"
```

**Escape-Characters | Steuerzeichen**
Ihn Python kann Text auch mit Escape-Characters formatiert werden, mit denen Zeilenumbrüche und Tabulatoren eingefügt werden können.
Die Anweisungen heißen Escape-Characters, da sie mit einem `\` beginnen.
- `\n`: Zeilenumbruch
- `\t`: Tabulator
#### f-Strings
Mit *f-strings* können Variablen durch geschweifte Klammern eingefügt, sowie Zahlen und Texte formatiert ausgegeben werden.
```python
print(f"text {x}")

text = "World"
print(f"Hello {text}")
```

**Formate**
Zahlen können in verschiedenen Formaten ausgegeben werden
- `f`: Zahlen werden mit einer Anzahl von Nachkomma, standardmäßig 6, ausgegeben
- `e`: Zahlen werden im Exponentialformat mit standardmäßig 6 Nachkommastellen ausgegeben
- `%`: Zahlen werden im Prozentformat mit standardmäßig 6 Nachkommastellen ausgegeben

Das Formatzeichen wird am Ende des f-Strings angegeben.
```Python
print(f"{x:f}")
print(f"{x:e}")
print(f"{x:%}")
```

**Zahlensysteme**
- `d`: Zahlen werden als Dezimalzahlen ausgegeben
- `b`: Zahlen werden als Binärzahlen ausgegeben
- `x`: Zahlen werden als Hexadezimalzahlen ausgegeben
- `o`: Zahlen werden als Oktalzahlen ausgegeben

```Python
print(f"{z:d}")
print(f"{z:b}")
print(f"{z:x}")
print(f"{z:o}")
```

**Nachkommastellen formatieren**
Um die Anzahl der Nachkommastellen zu formatieren.
```Python
print(f"{x:.anzNachkomma}")

x = 2.3456
print(f"{x:.2f})
>>> 2.35
```

**Stellenbreite formatieren**
Neben der Anzahl der Nachkommastellen kann man auch die Anzahl an Stellen bestimmen (rechtsbündig), was sich eignet um Tabellen zu erzeugen.
```Python
print(f"{x:anzZiffern})

print(f"{x:10}")
>>>   2.345600
```

**Rechts- und Linksbündig**
- `<`: Text wird linksbündig ausgegeben
- `>`: Text wird rechtsbündig ausgegeben

```Python
print(f"x:<")
print(f"x:>")
```
### .Format
Die Syntax entspricht der von f-Strings jedoch werden Platzhalter und nicht die Variablen in die geschweifte Klammern geschrieben
**Platzhalter**
`{}` dienen als Platzhalter für die Werte die nach dem String angegeben werden
```python
print("{} {}".format("Hello", "world")
```

Die Platzhalter können auch mit Parametern gefüllt werden.
```python
print("{dividend} / {divisor} = {quotient}".format(dividend = 20, divisor = 5, quotient = 20//5))
```

**Reihenfolge**
Man kann mit Angabe eines Index auch die Reihenfolge der Argumente bestimmen
```python
print("It is a {1}, {1} {0} world".format("world","mad"))
```

## Eingabe

Um Eingaben zu lesen wird die Funktion `input()` benutzt, die eingelesenen Daten sind dabei vom Datentyp String, um Eingaben als einen anderen Datentyp zu verwerten muss eine Typumwandlung stattfinden.
>[!info] Deaf Program
>A program that does not get a user's input is a *deaf program*.

```Python
print("Tell me a secret...")
anything = input()
print("Hmm...", anything, "... That is a good secret.")
```

Eingabe von Zahlen
```Python
zahl = int(input())
```
**Input Function with an Argument**
You can use the `input` function to give a prompt to the user without the `print` function.
```Python
x = input("text")

secret = input("Tell me a secret")
print("Hmmm...", secret, "I will not tell anyone.")
```

## Kommandozeilenargumente lesen
Um Argumente einzulesen die bei der Ausführung des Programms in die Kommandozeile eingegeben werden, benutzt man `argv` aus dem `sys` Modul.
Die Eingabe wird als Liste übergeben wobei der Name des Programms an erster stelle ist (`sys.argv[0]`). 
Weitere Argumente werden dann an die Liste hinzugefügt:
```Python
import sys

progName = sys.argv[0]
x = sys.argv[1]
y = sys.argv[2]
```

Für eine beliebige Menge von Input kann man ein Slice benutzen
```Python
x = sys.argv[1:]
```
# Operatoren

>[!note] Rangordnung der Operatoren
>- Exponent (`**`)
>- Bit-Komplement (`~`), Plus als Vorzeichen (`+`) und Minus als Vorzeichen (`-`)
>- Multiplikation (`*`), Division (`/`), ganzzahlige Division (`//`) und Modulo (`%`)
>- Addition (`+`) und Subtraktion (`-`)
>- Bit-Verschiebung nach links (`<<`) und nach rechts (`>>`)
>- bitweises Und (`&`)
>- bitweises Oder (`|`) und Exklusiv-Oder (`^`)
>- kleiner als (`<`), kleiner oder gleich (`<=`), größer als (`>`) und größer oder gleich (`>=`)
>- gleich (`==`) und ungleich (`!=`)
>- Zuweisungs- und Modifikationsoperatoren (`=`, `+=`, `-=`, `*=`, `/=` etc.)
>- Identität (`is`) und Nichtidentität (`is not`)
>- Element (`in`) und Nichtelement (`not in`)
>- logisches Und (`and`), logisches Oder (`or`) und logische Verneinung (`not`)

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
Mit Bitoperatoren kann man auf die binäre Darstellung von Daten zugreifen und Operationen durchführen.
![[Bitoperatoren.png|554x116]]
![[Bitoperatoren 2.png.png]]

## Relationale Operatoren (Vergleichsoperatoren)

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

# Verzweigungen
>[!note]
>Die Anweisung `pass` bewirkt, dass keine Anweisung ausgeführt wird. Dies wird benutzt wenn Verzweigung statt findet, aber bei dieser nicht passieren soll.
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

Zusätzlich ist es möglich mehrere Vergleichsoperatoren in eine Bedingung zu schreiben:
```Python
if x < y < z:
	print("y liegt zwischen x und z")
```

**Conditional Expression**
Ohne `elif` Anweisung kann die If-Verzweigung als *Conditional Expression* geschrieben werden:
```python
dannWert if Bedingung else sonstWert

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

- Mit `continue` wird ein Schleifendurchlauf abgebrochen und der nächste wird sofort ausgeführt.
- Mit `break` wird die gesamte Schleife abgebrochen.
## For-Schleife
For-Schleifen werden benutzt wenn Anweisungen für eine bekannte Anzahl von Wiederholungen ausgeführt werden sollen.
```python
for Variable in Aufzählung:
	Anweisung
	
for i in 1,6,5,4:
	if i*i > 20:
		break
	print(f"Zahl: {i}, Quadrat {i*i})
```

**Range**
Um durch einen Zahlenbereich zu iterieren wird `range()` benutzt
```python
for i in range(anfangsWert,endWert, intervall):
	Anweisung
	
for i in range(1,10,2):
	print(i)
	
for i in range(10,1,-2):
	print(i)
```

> [!note]
> - Der Endwert ist ausgeschlossen, d.h. dieser Wert wird nicht mehr ausgeführt.
> -  Sollte man keinen Intervall angeben wird der Wert 1 benutzt.
> - Wenn man nur eine Zahl angibt, wird diese als der Endwert betrachtet

**Elementoperator**
Diese Schleifen können benutzt werden um mit dem *Elementoperator* über Inhalte zu iterieren
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

**List-Comprehensions**
For-Schleifen können in eckigen Klammern als *List-Comprehensions* um Listen zu erzeugen
```python
gefilterte_liste = [ausdruck for element in liste]

numbers = list(range(1,6))
squares = [numbers ** 2 for number in numbers]
```

Zusätzlich kann dieser Ausdruck mit `if` benutzt werden um Listen zu filtern
```python
gefilterte_liste = [ausdruck for element in liste if bedingung]

evenNumbers = [number for number in numbers if number % 2 == 0]
>>> [2,4]
```

## While-Schleife
While-Schleifen werden benutzt wenn Anweisungen für eine unbekannte Anzahl von Wiederholungen ausgeführt werden sollen, bzw. wenn die Wiederholung einer Bedingung unterliegt.

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

# Fehler und Ausnahmen
Fehler entstehen oft wenn falsche Eingaben gemacht werden, etwa einen Text eingeben wenn eine Zahl erwartet wird.
Bei Fehlern werden *Exceptions* ausgelöst und führen zu einem Programmabsturz, wenn sie nicht abgefangen werden.

Es gibt drei Arten von Fehlern:
- *Syntaxfehler*:  Es wird nicht die korrekte Syntax benutzt
- *Laufzeitfehler*: Fehler zur Laufzeit, wie eine falsche Eingabe
- *Logische Fehler*: Fehler im Ablauf oder Reihenfolge des Programms und dessen Teile
## Try-Except
Zum abfangen wird `try-except` benutzt
```python
try:
	Anweisung
except Errortype:
	Anweisung bei Fehler
	
try:
	zahl = int(input())
	print("Es wurde die Zahl", zahl, " eingegeben")
except:
	print("Es wurde keine ganze Zahl eingegeben")
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

>[!note]
>Bei Ausnahmebehandlungen wird nur die kritische Zeile, etwa Eingabeaufforderung, Bearbeitung einer Datei oder Aufruf eines Gerätes, eingebettet und nicht ein ganzer Codeblock.
## Raise
In eigenem Code kann man `raise` benutzen um Ausnahmen auszulösen, dies kann man nutzen damit das Programm direkt zur `except` Anweisung springt.
```Python
raise 

try:
	zahl = input()
	if x < 0:
		raise 
except:
	Anweisung
```

Zudem kann man mit `raise` verschiedene Fehlertypen angeben und eine spezifische Ausgabe erzeugen.
```python
raise errorType("text")

def function(parameter: int):
	try:
		if type(parameter) is not int:
			raise RuntimeError("Argument muss Integer sein")
	except ValueError:
		Anweisungen
```
## Fehlerklassen
Zusätzlich kann man eigene Ausnahmeklassen von vorhandenen ableiten
```python
class OwnTypeError(TypeError):
	pass
	
def function(parameter):
	if Bedingung:
		raise OwnTypeError("Wrong datatype")
		Anweisungen
```

# Referenz, Identität und Kopie

>[!note]
>Mit dem Identitätsoperator `is` kann man überprüfen ob zwei Variablen auf dasselbe Objekt zeigen.
>```Python
>a is b
>```

Der Bezeichner eines Objekts ist nur eine Referenz auf ein Objekt. 
-> `x = 12`

Wird diese Referenz einem anderen Bezeichner zugewiesen, wird eine zweite Referenz erzeugt. 
-> `y = x`

Wird das Objekt über die zweite Referenz geändert dann,
- wird bei einfachen Objekten (Zahl oder String) ein weiteres Objekt erzeugt in dieser der neue Wert gespeichert wird.
- wird bei nicht-einfachen Objekten (Liste, Dictionaries, usw.) wird das original Objekt geändert.

>[!note]
>Wenn ein Objekt über eine Referenz ein Wert zugewiesen wird und eine andere Referenz auf diesen Wert besteht, können beide Referenzen auf dasselbe Objekt verweisen. 
>Dies geschieht um Speicherplatz zu sparen.

`del` wird benutzt um Referenzen zu löschen. 
Bei mehreren Referenzen wird das Objekt durch Löschen einer Referenz nicht gelöscht.

Um eine Kopie von komplexen Objekten zu erzeugen kann `copy.deepcopy()` benutzt werden.
```Python
y = copy.deepcopy(x)
```
# Funktionen
Funktionen helfen Code zu modularisieren und dessen Wiederverwendbarkeit zu erhöhen.

>[!note]
>Funktionen können in Python nicht überladen werden, d.h. zwei Funktionen haben den gleichen Namen, aber andere Parameter / Definition. 

Um eine Funktion zu definieren wird die Anweisung `def` benutzt, gefolgt von einem Bezeichner
```Python
def funktionsname():
	Anweisung
```

> [!NOTE]
> Die Anweisung `pass` bewirkt, dass keine Anweisung ausgeführt wird. Dies wird unter anderem für Funktionsprototypen benutzt, die noch keine Anweisungen haben oder noch nicht fertig sind.

**Parameter**
Um Werte an eine Funktion zu übergeben werden Parameter benutzt, welche in die Klammern nach dem Bezeichner der Funktion geschrieben werden.
```Python
def funktionsname(x, y):
	Anweisung
```

Um einer Funktion eine variable Anzahl von Parametern zu übergeben wird ein Stern `*` vor die Variable gesetzt. In dieser wird ein Tupel mit den jeweiligen Werten gespeichert.
Bei mehreren Parametern wird die Variabel als letztes angegeben.
```Python
def funk(*parameter)

def funk(parameter1, ..., *parameterN)
```

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

Man kann auch Funktionen als Parameter angeben und als Argumente übergeben.
```Python
def funk1(funkPara)
	Anweisung
	funkPara()
	

funk1(funk2)
```

**Rückgabewerte**
Wenn eine Methode einen Wert zurückgeben soll wird `return` benutzt, dabei muss man auch nicht im Funktionskopf den Typ des Rückgabewerts angeben.
```python
def funktion()
	return x
```

Des Weiteren ist es in Python möglich mehrere Rückgabewerte zu liefern, die Werte werden mit einem Komma getrennt nach die `return` Anweisung geschrieben und als Tupel zurückgegeben.
```Python
def funk()
	return x,y
```

Zu beachten ist, dass die Anzahl der Variablen, an die die Werte zurückgegeben werden, mit der Anzahl der Werte übereinstimmt.
```Python
a, b = funk()
```

**Type-Hints**
Um in Python den Datentyp von Parametern oder Rückgabewerten festzulegen werden *Type-Hints* benutzt.
Für Parameter wird der Datentyp nach dem Parameternamen und einem Doppelpunkt geschrieben, für Rückgabewerte wird der Datentyp mit einem Pfeil ans Ende des Methodenkopfes geschrieben.
```python
def funktion(parameter: datentyp) -> DatentypRückgabe:
	Anweisungen
```

**Rekursive Funktionen**
Bei bestimmten Abläufen lohnen sich rekursive Funktionen, also Funktionen die sich selber aufrufen bis eine bestimmte Bedingung erfüllt ist.
```Python
def funk()
	Anweisung 
	if Bedingung:
		funk()
```

**Lambda Funktionen**
Mit Lambda Funktionen ist es möglich Funktionsdefinitionen zu verkürzen, diese dürfen jedoch keine Mehrfachanweisungen, Ausgaben oder Schleifen beinhalten.
```Python
x = lambda Parameter: Anweisung

plus = lambda x,y: x+y
```

## Eingebaute Funktionen
-  `abs()`: Liefert den Betrag einer Zahl 
- `exec()`: Führt einen Befehl aus 
- `filter()`: 

# Dateien und Verzeichnisse
Das Modul `sys` stellt Funktionen zur Arbeit mit Dateien bereit.

**Zugriff und Dateityp**
- Sequenzieller Zugriff:
  Die Zeilen werden sequenziell (nach einander) gelesen und geschrieben, der Zugriff auf eine bestimmte Zeile ist nicht direkt möglich
- Wahlfreier Zugriff:
  Die Zeilen können direkt gelesen und geschrieben werden
- Binärer Zugriff:
  Die einzelnen Bytes der Datei können gelesen und geschrieben werden

**Öffnen von Dateien**
Für den Zugriff auf Dateien werden diese mit `open()` geöffnet, dadurch wird ein Objekt erstellt dessen Methoden zum Lesen und Schreiben in der Datei verwendet wird.
```python
varName = open("datei", "mode = x")


import sys
# Absoluter Pfad
datei = open("/Users/Name/file.txt", "mode = r")

# relativer Pfad (Datei ist im selben Ordner)
datei = open("file.txt", "mode = w")
datei.write("Das wird in die Datei geschrieben")
datei.close()
```

>[!warning]
>Nach der Bearbeitung muss die Datei mit `close()` geschlossen werden, sonst kann es sein, das ein weiterer Zugriff nicht möglich ist.

Der Mode beschreibt was mit der Datei gemacht wird:

| **Mode** | **Description**                                   | **If file does not exist** |
| -------- | ------------------------------------------------- | -------------------------- |
| `r`      | Read only, get entire content                     | FileNotFoundError          |
| `w`      | Write at the start of the file, overwrite content | Creates file               |
| `a`      | Append at the end of the file                     | Creates file               |
| `x`      | Create                                            |                            |
| `r+`     | Read and Write (at the start)                     |                            |
| `w+`     | Write and Read; File will be cleared              |                            |
| `a+`     | Append and Read                                   |                            |
| `b`      | Read and Write in binary                          |                            |
Um die Datei im Binärmodus zu benutzten kann man ein `b` an den Modus anhängen.
`wb` -> Write in binary

**File Cursor**
Jedes Dateiobjekt benutzt einen *File Cursor* der die aktuelle Zugriffsposition markiert und mit jedem Lese- und Schreibvorgang verändert.
Mit `seek(position)` kann der Zeiger auf eine andere Position gesetzt werden.
```python
file.seek(2)
```

>[!note]
>Escape-Characters wie Zeilenumbrüche werden auch mitgezählt

**Iterator**
Das Datei-Objekt stellt für Textdateien einen Iterator bereit, mit dem man die Datei zeilenweise auslesen kann.
```python
for line in file:
	print(line.strip())
```

**Informationen über Dateien**
Mit `stat()` aus dem Modul `os` kann man Informationen von Dateien auslesen
- https://www.geeksforgeeks.org/python/python-os-stat-method/

Die Daten können als Tupel abgerufen werden oder über die Angabe des Attributs.
Um Informationen mit Zeitangaben zu formatieren kann man `localtime` und `strftime` benutzen.
```Python
stat = os.stat("file.xy")
sizeTup = stat[6]
sizeAtt = stat.st_size
```
## Lesen und Schreiben
**Schreiben**
Um in eine sequenzielle Datei zu schreiben muss diese mit `open()` im Modus `w`, `a` oder `a+` geöffnet werden. Zum schreiben kann man folgende Funktionen nutzen:
- `write()`: schreibt einen einzelnen String in die Datei
- `writeline()`: schreibt eine Liste von Strings in die Datei
```Python
import sys

file = open("file.txt", "w")
file.write("text")
texte = ["Hello", str(2000), "xyz"]
file.wirteline(texte)
file.close()
```

**Lesen**
Um eine sequenzielle Datei zu lesen muss diese mit `open()` im Modus `r` oder `r+` geöffnet werden.
Zum lesen der Datei stehen folgende Funktionen bereit:
- `read()`: liefert den Inhalt der Datei als einen einzigen String zurück
- `readlines()`: gibt alle Zeilen als eine Liste von Strings zurück
- `readline()`:  liest pro Aufruf eine Zeile aus der Datei und erhöht den File Cursor

>[!note]
>Man kann als Parameter eine Zahl angeben, die besagt wie viele Bytes gelesen werden sollen
>`file.read(4)` -> Es werden 4 Bytes gelesen
>(Jedes Zeichen ist ein Byte lang)

```Python
import sys

datei = open("file.txt")

text1 = datei.read()
print(text1)

text2 = datei.readlines()
for zeile in text2:
	print(zeile, end="")
	
text3 = datei.readline()
print(text3)
```

### formatierte Dateien
Eine Datei ist formatiert, wenn der Inhalt in einer Struktur festgelegt ist und somit genau bekannt ist an welcher Stelle welche Informationen stehen, wodurch man auf diese zugreifen und verändern kann ohne den restlichen Inhalt zu beeinflussen.

**Schreiben**
Um in eine Datei formatiert zu schreiben, benutzt man formatierte Strings wie `.format()` oder f-Strings. 
## CSV Dateien
[[(CSV) Comma-Separated Values]] 
 
**Schreiben**
Um in eine CSV Datei zu schreiben muss diese zu erst geöffnet werden.
Da in CSV Dateien pro Zeile ein Datensatz steht und die Werte getrennt werden kann man Listen von Werten benutzen. 
Zahlen müssen in Strings umgewandelt werden.
```Python
import sys
datei = open("file.csv","w")

liste = [43, "Müller", 10.5]
datei.write(str(liste[0]) + ";" + liste[1] + str(liste[2]) + "\n")

liste2 = [[43, "Müller", 10.5], [42, "Miller", 10.4]]
for element in liste2:
	datei.write(str(element[0]) + ";" + element[1] + str(element[2]) + "\n")
```

**Lesen**
Um eine CSV Datei zu lesen müssen die Struktur und die Datentypen bekannt sein und die einzelnen Zeilen getrennt werden.
```Python
datei = open("file.csv")
text = datei.read()
zeilen = text.split(chr(10)) 
```

## Serialisierung
*Serialisierung* speichert ein Objekt als Bytefolge in eine Datei, wenn ein Objekt aus einer Datei geladen wird spricht von *Deserialisierung*.

Das Modul `pickle` stellt Methoden zur Serialisierung und Deserialisierung bereit.

**Serialisierung**
Zur Speicherung von Objekten in Dateien wird die Methode `dump()` benutzt.
Die Datei muss davor zuerst im Modus `wb`, zum Schreiben im Binärmodus, geöffnet werden.

```Python
import pickle, sys

file = open("datei.bin", "wb")

pickle.dump(obj, file)
```

Neben Objekten aus der OOP, können auch Datenobjekte wie Strings usw. gespeichert werden.

**Deserialisierung**
Mit `load()` kann man nacheinander Objekte die mit `dump()` in eine Datei geschrieben wurde laden.
Bei Objekten aus eigenen Klassen muss die Definition bekannt sein und die Datei im Modus `rb` (read binary) geöffnet werden.

```Python
import pickle, sys

file = open("datei", "rb")
obj1 = pickle.load(file)
file.close()
```
## Suchen von Dateien und Inhalten
**glob()**
Die Funktion `glob()` aus dem Modul `glob` kann benutzt werden um nach Dateien (im aktuellen Verzeichnis) zu suchen und diese in einer Liste zu speichern.
```Python
files = glob.glob("name.xy")
```

Man kann es auch benutzen um nach einem Muster oder regulären Ausdrücken zu suchen :
- `*`: Platzhalter für mehrere beliebige Buchstaben
- `?`: Platzhalter für einen beliebigen Buchstaben

```Python
files = glob.glob("regEx.xy")

import glob
files1 = glob.glob("ob*.txt")
>>> obst.txt, ober.txt, objekt.txt
files2 = glob.glob("[HM]aus.txt")
>>> Haus.txt, Maus.txt
```

Um in Unterverzeichnissen oder den gesamten Verzeichnisbaum zu durchsuchen benutzt man
- `glob.glob("**/file.xy")`: durchsucht nur direkte Unterverzeichnisse
- `glob.glob("**/file.xy", recursive=True)`: durchsucht den gesamten Verzeichnisbaum (direkte Unterverzeichnisse, deren Unterverzeichnisse, usw.)

**scandir()**
- https://www.geeksforgeeks.org/python/python-os-scandir-method/

Alternativ kann man auch die Funktion `scandir()` aus dem Modul `os` benutzen um ein Verzeichnis zu durchsuchen.
Als Parameter erwartet die Funktion einen Pfad und liefert ein iterierbares Objekt vom Typ `os.DirEntry` zurück der alle Einträge des Verzeichnis enthält.
Man muss am Ende die Variable von `scandir()` schließen um den Zugriff auf das Verzeichnis wieder freizugeben.
Um das aktuelle Verzeichnis zu durchsuchen kann man `.` angeben.

```Python
files = os.scandir("path")
files.close()
```

> [!tip]
> Um nach einem bestimmten Eintrag zu suchen muss man das Objekt durchlaufen und nach dem Namen mit String Methods suchen.
> z.B.:
> ```Python
> for x in files:
> 	if x.name.startswith('ob') and x.name.endswith('.py'):
> 		file = open(x)
> ```

**Verzeichnisinhalt ausgeben**
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

## Verwaltung von Dateien
Die Module `os` und `shutil` bieten Funktionen zur Verwaltung von Dateien
**Existenz überprüfen**
```Python
if os.path.exists("file.xy"):
	print("Exists")
else:
	print("Does not exist")
```

**Datei kopieren**
```Python
shutil.copy("file.xy", "copyFile.xy")
```

**Datei umbenennen**
```Python
shutil.move("file.xy","newName.xy")
```

**Datei entfernen**
```Python
os.remove("file.xy")
```

# OOP
## Klasse
In Klassen werden die Eigenschaften und Funktionen von Objekten gespeichert.

Um eine Klasse in Python zu erzeugen benutzt man:
```python
class Name:
	
	# Eigenschaften
	x = xx
	y = yy

	# Konstruktor
	def __init__(self,x,y):
		self.x = x
		self.y = y
	
	# Destruktor
	def __del__(self):
	Anweisung
	
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

Methoden sind ähnlich wie Funktionen und bestimmen was ein Objekt ausführen kann.
```Python
def meth(self,x)
	Anweisung
```

>[!note]
>Klassenmethoden haben immer den Parameter `self` an erster Stelle, wobei der Name geändert werden kann.

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

Es stehen vordefinierte Methoden zur Verfügung
- `__ge__()`: greater equal >=
- `__lt__()`: lower than <
- `__le__()`: lower equal <=
- `__ne__()`: not equal !=
- `__add__()`: add +
- `__mul__()`: multiply *
- `__truediv__()`: div /
- `__floordiv__()`: //
- `__mod__()`: modulo %
- `__pow__()`: power ** 
### Konstruktor und Destruktor
- *Konstruktoren* werden benutzt um Objekten bei deren Erstellung Werte zuzuweisen
- *Destruktoren* werden benutzt um Aktionen beim Lebensende eines Objekts auszulösen

Die Syntax für Konstruktoren und Destruktoren ist:
```Python
def __init__(self,x,y):
	Anweisung
	
def __del__(self):
	Anweisung
```
## Vererbung
Klassen können ihre Eigenschaften und Methoden an andere Klassen vererben, wodurch die Child-klasse die Methoden benutzen oder überschreiben kann.
Da für wird der Name der abzuleitenden Klasse in Klammern hinter den Klassennamen geschrieben:
```python
class ChildClass(ParentClass):
	Definition
```

Mit `super` können die Methoden der Elternklasse aus der Kind-Klasse aufgerufen werden.
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

# Regular Expressions
Reguläre Ausdrücke sind Teil-String die im gesuchten Strings enthalten sind und werden benutzt um bestimmte Texte, Textteile oder einzelne Zeichen zu suchen oder zu ersetzten. So können sie bei der Kontrolle von Benutzereingaben oder bei der Suche nach Dateien eingesetzt werden.
Zum Arbeiten mit regulären Ausdrücken wird das Modul `re` benutzt.

>[!note]
>RegEx können auch mit Ziffern und Sonderzeichen benutzt werden

Die Teil-Strings werden als Muster angegeben
- `abc`: gibt die gesuchten Zeichen oder Wort aus
  `ee`-> Tee, See, Teer
- `[ab]`: steht für ein Zeichen aus der Liste
  `[HM]aus`-> Haus, Maus
- `[a-z]`: steht für den angegebenen Zeichenbereich; auch Zahlen können angegeben werden
- `[^abc]`: steht für jedes beliebige Zeichen ausgeschlossen den Zeichen aus der Liste
  `[^M]aus` -> Haus, raus 
- `.`: steht für genau ein beliebiges Zeichen
  `.aus`-> Haus, Maus, raus
- `^`: Es werden nur Teiltexte die am Anfang des Strings stehen untersucht
  `^abc`
- `$`: Es werden nur Teiltexte die am Ende des Strings stehen untersucht
  `abc$`

Zusätzlich gibt es *Quantifiers* mit denen man die RegEx modifizieren kann.
- `?`: die linksstehende RegEx ist optional
  `Hau?se`-> Hase, Hause
- `*`: die linke RegEx kann beliebig oft (keinmal, einmal oder mehrmal) vorkommen
  `12*3`-> 13,123,122223,...
- `+`: die linke RegEx kommt mindestens einmal vor
  `12+3`-> 123,1223,12223,...
- `{x}`:  die linke RegEx muss x mal vorkommen
  `[1-9]{5}`-> fünf Ziffern zwischen 1 und 9
- `{m,n}`:  die linke RegEx kommt mindestens `n` und maximal m mal vor

**Suchen**
- `re.search()` sucht in dem gesamten String nach einem Treffer 
- `re.match()` überprüft nur den Anfang des Strings
- `re.findall()` liefert ein Tupel von mehreren zutreffenden Strings zurück

Mit `search()` kann man in einem String nach einem regulären Ausdruck suchen. 
Sollte ein Treffer gefunden werden wird ein Match-Objekt zurück geliefert, falls es keinen gibt erhält man `None`. 
```python
x = re.search("regEx", text)

firstVowel = re.search("[aeiou]", "Hello")
>>> 'e'
```

`findall()` wird nach allen regulären Ausdrücken in einem Text gesucht und als Tupel zurückgegeben.
```Python
x = re.findall("regEx", text)

text = "Haus und Maus und Laus"
x = re.findall("[HM]aus", text)
>>> ['Haus','Maus']
```

Mit `span()` wird ein Tupel zurück geliefert das die Anfangsposition und die erste Position die nicht mehr zum Treffer gehört.
```python
firstVowel.span()
>>> (1,2)
```

**Ersetzen**
Mit `sub()` kann man einen Textteil, der einer RegEx entspricht, durch einen anderen Text ersetzen.
```Python
re.sub("regEx", "newText", string)

x = re.sub("Maus", "raus", text)
```

**Iterator**
With `finditer()` a iterator object is created, which processes a text until a match is found and only processes further when passed to the `next` function. 
```Python
x = re.finditer("regEx", string)
next(x)
```

The iterator can also be used with a for loop
# Systemnahe Programmierung
## Prozesse
Mit dem Befehl `fork()` aus dem `os` Modul kann man in Unix Systemen einen neuen [[Betriebssysteme - Operating Systems#Prozessverwaltung|Prozess]] erzeugen, der eine identische Kopie eines ursprünglichen Prozesses erstellt. 
Die Prozesse werden dann eingesetzt um unterschiedliche Aufgaben zu erfüllen, um sie zu unterscheiden gibt `fork()` im ursprünglichen *Parent* Prozess die Prozess ID des *Child* Prozesses zurück und im Child Prozess `0`. 
```python
import os

pid = os.fork()

if pid == 0:
	print("Child process")
else:
	print("Parent process. Child: {}".format(pid))
```

## Pipes
[[Betriebssysteme - Operating Systems#Pipes|Pipes]] werden durch den Befehl `os.fork()` erzeugt wobei zwei Variablen zugewiesen werden müssen.
```python
reader, writer = os.pipe()
```

## Threads
Das Modul `threading` bietet Funktionen zum Erstellen und Arbeiten mit [[Betriebssysteme - Operating Systems#Threads|Threads]].
Threads haben Zugriff auf alle globalen Daten und Objekte des übergeordneten Threads.

**Erzeugung von Threads**
Um einen Thread zu erzeugen muss ein Objekt der Klasse `Thread` erstellt werden und dessen Konstruktor per `target=` den Namen einer Callback-Funktion übermitteln die in dem Thread ausgeführt werden soll. 
Um den Thread zu starten wird die Funktion `start()` verwendet.

```Python
x = threading.Thread(target= y)
x.start()
```

**Identifizierung eines Threads**
Jeder Thread hat eine individuelle ID, mit `get_ident()` wird die ID des aktuellen Threads ermittelt.
```Python
x = threading.get_ident()
```

**Exceptions**
Tritt ein Fehler  wird eine Exception nur in dem betreffenden Thread ausgelöst, alle anderen Threads werden nicht betroffen.
# Network
## Sockets

**Sockets erzeugen**
>[!note]
>An beiden Enden einer Netzwerkverbindung befinden sich zwei Sockets, die vergleichbar sind wie die Telefone in einer Telefonverbindung.

Um Sockets zu verwenden muss das Modul `socket` importiert werden.

Um ein Socket zu erzeugen benutzt man den Befehl
```python
sock = socket.socket(domain, type, protocol)

import socket

# TCP socket
tcpSock = socket.socket(
	socket.AF_INET,
	socket.SOCK_STREAM,
	socket.getprotobyname('tcp')
)

# UDP socket
udpSock = socket.socket(
	socket.AF_INET,
	socket.SOCK.DGRAM,
	socket.getprotobyname('udp')
)
```

**Adressen und Ports**
- `socket.gethostbyname(hostname)`
  wandelt den hostnamen in die entsprechende IP Adresse um, benötigt jedoch Zugriff auf einen DNS-Dienst oder Server; Rückgabewert ist der Hostname und die IP-Adresse in ASCII Zeichen
- `socket.getservbyname(service, protocol)`
  statt der Portnummer kann das bei den "Well-known" Ports der Dienst und das Transportprotokoll angegeben werden
  ```python
  port = socket.getservbyname('ftp', 'tcp')
  ```

**Verbindungen und Datenaustausch**
- **UDP**
Bei einem UDP Socket kann man nach der Erstellung Daten sofort Senden und Empfangen benutzt 
	- `sock.bind((destAddr, port))`
	  stellt eine Verbindung zu einem UDP Host her, angegeben als Tupel aus IP-Adresse und Port
	- `sock.sendto(message, (addr,port))` 
	  sendet die Daten an den Empfänger; der Empfänger wird als Tupel bestehend aus IP-Adresse und Port angegeben, z.B. `("192.168.0.4", 8000)`
	- `sock.recvfrom(buffersize)`
	  empfängt ein UDP-Datagramm; `buffersize` gibt die Größe des Lesepuffers in Integer an; gespeichert wird das Paket in zwei Variablen, eine für die Daten und eine für die IP-Adresse des Senders

- **TCP**
	- `sock.connect(dest)`
	  stellt eine Verbindung zu einem TCP Host her
	- `sock.send(binary)`
	  sendet einen Binär-String der nur aus ASCII Zeichen bestehen darf
	- `sock.recv(buffersize)`
	  wartet auf Daten vom Host und nimmt Daten in Größe des buffersize auf in Form eines Binärstrings
	- `sock.bind((addr,port))`
	  bindet ein Socket an eine IP-Adresse und einen Port
	- `sock.listen(max_queue)`
	  wandelt ein mit `bind()` gebundenes Socket ein lauschendes um und wartet auf einen Verbindungsversuch; `max_queue` gibt die maximale Größe der Warteschlange von Clientverbindungen an
	- `(clientsocket, remote_addr) = sock.sccept()`
	  wenn eine Verbindung eingeht, wird der Rest des Programms bzw. die nächste Programmzeile ausgeführt

## Internet
Das Modul `urllib` enthält Untermodule die zum Laden und Senden von Daten aus und in das Internet.
### Daten aus dem Internet
Das Untermodul `urllib.request` stellt Funktionen zum lesen und laden von Daten aus dem Internet bereit

- **urlopen()**: speichert den Inhalt einer URL als Byte Liste in eine Variable
```Python
x = urllib.request.urlopen("URL")
x.close()
```
>[!tip]
>Die Liste kann wie eine Datei mit z.B. `readlines()` eingelesen werden 

- **urlretrieve()**:  speichert den Inhalt einer URL in einer Datei ab
```Python
urllib.request.urlretrive("URL","Path/to/file")
```

# Module
Module stellen vordefinierte Funktionen zur Verfügung.
## Eigene Module 
Um eigene Module zu erstellen werden die gewünschten  Funktionen und Code in eine eigene Datei geschrieben, wobei der Dateiname gleichzeitig der Name des Moduls ist.
Das Modul kann dann mit `import Modulname` importiert und benutzt werden, sofern sich beide im selben Verzeichnis befinden.
## Import
Um Module zu importieren wird `import` benutzt:
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

# Externe Module
Python Module sind in dem [Python Package Index (PyPI)](https://pypi.org/) verfügbar, diese können mit `pip` und für Python 3 `pip3` installiert, aktualisiert und deinstalliert werden.
## NumPy
Dieses Modul ist für das Rechnen und Operieren mit Arrays optimiert und deswegen auch für lineare Algebra geeignet. 

> [!NOTE]
> Es wird für Machine Learning eingesetzt und ist Teil von *Scientific Python (SciPy)* einer Sammlung von wissenschaftlich-mathematischen Modulen.

### Arrays
Um (mehrdimensionale) Arrays zu erzeugen benutzt man `numpy.array([array])`
```python
import numpy

a1 = numpy.array([3,2,1])
a2 = numpy.array([3,2,1][-1,-2,-3])

print(a1)
print(a2[1])
print(a2[1][2])
print(a2[1,2])
```

Man kann auch *Vektoren* darstellen
```python
# Spaltenvektor
sv = numpy.array([[1],[2],[3]])

# Zeilenvektor
zv = numpy.array([1,2,3])
```

*Matrizen* können nach folgendem Schema erstellt werden
```python
m1 = numpy.array([[1,2,3],[-1,-2,-3]])
```

*Skalarmultiplikationen* können mit dem normalen Multiplikationsoperator durchgeführt werden
```python
m1 * 4
sv * -5
```

Um Skalar- und Punktprodukte zu berechnen wird die Funktion `.dot()` benutzt. 
Mit ihr kann auch die Matrixmultiplikation nach dem Falk-Schema durchgeführt werden
```python
numpy.dot(zv1,zv2)
zv1.dot(zv2)

m1.dot(m2)
```

Spaltenvektoren müssen mit `transpose()` erst transponiert werden bevor man das Skalarprodukt berechnen kann. Mit dieser Funktion kann man auch Matrizen transponieren.
```python
sv.transpose()
m1.transpose()
```

Nuller Matrizen können mit `.zeros()` erstellt werden
```python
numpy.zeros([3,4])
```

## math 
In diesem Modul befinden sich mathematische Funktionen 
- https://docs.python.org/3/library/math.html

# Statistik
Das Modul `statistics` stellt Funktionen für Statistik bereit.
- Median: `statistics.median()`
- unterer Median: `statistics.median_low()`
- oberer Median: `statistics.median_high()`
- Arithmetischer Mittelwert: `statistics.mean()`
- Harmonischer Mittelwert: `statistics.harmonix_mean()`

# Datenanalyse
Python kann auch für [[Abominable Intelligence – Silica Animus#Datenanalyse|Datenanalyse]] benutzt werden.

> [!NOTE]
> Jupyter Notebooks sind praktisch im Arbeiten mit Datenanalyse

## Aufbereitung 
### Bag of Words
Um einen Text als [[Abominable Intelligence – Silica Animus#Bag of Words|Bag of Words ]]zu formatieren kann man die Klasse `CountVectorizer`, aus dem Modul `scikit-learn`, benutzen.
```python
from sklearn.feature_extraction.txt import CountVectorizer
import numpy

strings = ["Berlin ist eine Stadt", "Berliner ist ein Gebäck", "JFK ist ein Berliner"]
# Als Eingabe ist ein Numpy Array mit den einzelnen Strings erforderlich
string_data = numpy.array(strings)
vectorizer = CountVectorizer()
bag_of_words = vectorizer.fit_transform(string_data)
```

In der Variable `bag_of_words` wird eine *Sparse Matrix* gespeichert, ein Format indem nur die Felder die nicht 0 sind gespeichert werden.
Um diese Matrix in ein NumPy Array zu wandeln benutzt man `.toarray()`
```python
bag_of_words.toarray()
```

Die Liste der Wörter auf die sich das Array bezieht, kann aus dem `CountVectorizer` Objekt abgerufen werden.
```python
vectorizer.get_feature_names_out()
```

Um *Stoppwörter* zu filtern kann man das Argument `stop_words` des Konstruktors von `CountVectorizer` eine Liste von Wörtern übergibt.
```python
stop = ["der", "die", "das", "ein", "eine"]
vectorizer = CountVectorizer(stop_words = stop)
```

Um einen Schwellenwert zu setzen ab dem Wörter herausgefiltert werden, kann man die im Konstruktor von `CountVectorizer` enthaltenen `min_df()` für die selten und `max_df()` für die häufig vorkommenden Wörter mit einem Wert zwischen 0 und 1 belegen.
```python
vectorizer = CountVectorizer(stop_words, max_df = 0.9)
```

### N-Gramme
Für [[Abominable Intelligence – Silica Animus#N-Gramme|N-Gramme]] kann auch die Klasse `CountVectorizer` benutzt werden. Dazu gibt man die Länge der gesuchten N-Gramme als Tupel `(minRange,maxRange)` an den Parameter `ngram_range` des Konstruktors überliefert werden.
```python
# einzelne Wörter und Bigramme
nGram1 = CountVectorizer(ngram_range= (1,2))
# Nur Bigramme
nGram2 = CountVectorizer(ngram_range= (2,2))
```

### Texte
Um längere Texte für die Verarbeitung mit Machine Learning Algorithmen vorzubereiten, kann man die Klasse `HashingVectorizer` aus dem Modul `sklearn.feature_extraction.text` verwenden.
Zusätzlich kann mit `HashingVectorizer` die Anzahl der gewünschten Features angegeben werden indem man die Anzahl an den Parameter `n_features` übergibt.
```python
from sklearn.feature_extraction.text import HashingVectorizer
import numpy
text_data = numpy.array(text)
hashvalue= HaschinVectorizer(n_features= 10)
features= hashvalue.transform(text_data)
features.toarray()
```

### Bilddateien
Für die Verarbeitung von Bilddateien eignet sich das Modul `scikit-image`
```python
from skimage.io import imread, imshow
image = imread("bild.jpg")
imshow(image)
```
Das Bild wird hier als dreidimensionales Array gespeichert, in dem für jedes Pixel die Farbwerte Rot, Grün und Blau als Integer zwischen 0 und 255 gespeichert wird.

>[!note]
>Um die Dimensionen des Arrays abzurufen wird `image.shape()` benutzt.

Um die Wertemengen zu reduzieren gibt es mehrere Möglichkeiten.

**Graustufen verwenden**
Eine Möglichkeit die Werte zu reduzieren ist es das Bild in Graustufen zu speichern, welche als 256 verschiedene Graustufen als Floats zwischen 0 und 1 gespeichert werden.
Hierfür benutzt man das Argument `as_gray`
```python
from skimage.io import imread, imshow
image = imread("bild.jpg", as_gray= True)
imshow(image)
```

**Bildausschnitt betrachten**
Es ist nicht immer erforderlich das Gesamtbild zu betrachten, deswegen ist es sinnvoll nur den relevanten Bildausschnitt zu verwerten.
Dafür werden die gewünschten Dimensionen als Koordinaten `[YStart:YEnde, XStart:XEnde]` angegeben
```python
ausschnitt= image[350:550, 250:450]
```

>[!note]
>Bei der Verarbeitung von mehreren Bildern sollten sie die gleichen Proportionen haben.

**Bild verkleinern**
Zusätzlich kann das Bild verkleinert werden, d.h. die Anzahl der Pixel wird verringert.
Dazu kann man die Funktion `resize()` aus dem Untermodul `skimage.transform` und übergibt das Bild und die gewünschte Größe, als Tupel, in Pixel.
```python
# Bild wird auf 50x50 Pixel verkleinert
verkleinert= resize(Ausschnitt, (50,50))
```
## Datenanalyse 
Zur Analyse von Datenmengen kann das Modul [pandas](https://pandas.pydata.org/docs/user_guide/index.html) benutzt werden.
>[!note]
>`pandas` benutzt die Datenstruktur DataFrame, eine Mischung aus Array und Datenbanktabelle, also eine Datenmenge mit mehreren Datensätzen.

Man kann verschiedene Dateiformate benutzen, jedoch sind [[(CSV) Comma-Separated Values]] sehr gut geeignet und der Header mit den Spaltentiteln wird automatisch als Schlüssel für den Zugriff auf die einzelnen Spalten verwendet. 

>[!note]
>Um eine CSV Datei ohne Header zu importieren muss das Argument `header= None` übergeben werden.

>[!note]
>Als Beispiel wird ein Auszug des [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set) benutzt.

Um eine Datei zu importieren wird `read_csv()` benutzt
```python
import pandas

iris = pandas.read_csv('iris.csv')
```

Mit `head(AnzahlZeilen)` kann man eine Anzahl von Zeilen der Datenmenge anzeigen lassen.
```python
iris.head(6)
```

Mit `.info()` kann man Informationen über die Datenmenge wie die Spaltentitel und Datentypen erfahren
```python
iris.info()
```

Um auf einzelne Spalten zuzugreifen wird der Spaltenname benutzt 
```python
iris['PetalWidth']
```

Beim Zugriff auf die Spalten und auch auf das DataFrame Objekt selbst kann man zusätzlich bestimmte Optionen festlegen:
- `.unique()`: die unterschiedlichen Werte
- `.min()`: der kleinste Wert
- `.max()`: der größte Wert
- `.mean()`:  der Durschnitt der Werte
- `.median()`: der Median der Werte

```python
# Zeigt die größten Werte aller Spalten an
iris.max()

# Zeigt den größten Wert für die Breite der Blüte an
iris['PetalWidth'].max()
```

Um die Werte sortiert auszugeben kann man `.grouby(Spaltenname)` benutzen
```python
iris.groupby('Classification')
```

Auf den Indexoperator kann man auch Vergleichsoperatoren anwenden
```python
iris[iris['Classification']== 'Iris-virginica']
iris[iris['PetalLength']> 2.3]
```

## Visualisierung
Mit dem Modul `matplotlib.pyplot` ist es möglichverschiedene Diagrammtypen zu erstellen um Datenmengen zu visualisieren.
Des Weiteren bietet das Modul [seaborn](https://seaborn.pydata.org/) mehr Darstellungen mit weniger Code darzustellen.

Ein einfacher Scatter-Plot lässt sich mit der `scatterplot()` Funktion erstellen
```python
import seaborn 
seaborn.scatterplot(
	data=iris, x='PetalLength', y='PetalWidth',
	hue='Classification', style= 'Classification'
)
```

Die Optionen `hue` und `style` sind für die Marker und Farben der Datenpunkte verantwortlich, `Classification` sorgt dafür, dass sich die Punkte in beiden Eigenschaften unterscheiden sollen. 

Box-Plots stellen die Werteverteilung eines Features der verschiedenen Kategorien dar.
```python
seaborn.boxplot(x='Classification',y= 'PetalLength', data= iris)
```

Ein Pair-Plot stellt Scatter-Plots für jede Kombination von Kategorien dar, wobei in den Feldern in denen sich dieselbe Kategorie überschneidet werden die möglichen Werte und die Häufigkeitsverteilung angegeben.
```python
seaborn.pairplot(data= iris, kind='scatter', hue='Classification'4)
```

Die Heatmap stellt die Korrelationen der verschiedenen Features dar, die mit der Funktion `.corr()` berechnet werden können. 
>[!note]
>Die Korrelation wird durch einen Wert zwischen +1 und -1 angezeigt, ein positiver Wert bedeutet, dass sich die Werte in dieselbe Richtung entwickeln, negative Werte, dass sie sich in unterschiedliche Richtungen entwickeln und 0, dass es keine Relation gibt.

```python
iris.corr()
seaborn.heatmap(iris.corr(), annot=True, cmap= 'viridis')
```

# Datum und Zeit
Das Modul `time` stellt Funktionen zur Verarbeitung und Formatierung von Datums- und Zeitangaben bereit.
Als Nullpunkt wird bei vielen Betriebssystemen der 1.Januar.1970 00:00 Uhr verwendet und die Zeit wird in Sekunden ab diesem Zeitpunkt gerechnet.

- **time()**: liefert die Zeit seit dem Nullpunkt in Sekunden zurück
  `time.time()`
- **localtime()**: liefert die aktuelle Zeit als Tupel zurück `[jahr,monat,tag,stunde,minute,sekunde]`
  `x = time.localtime()`
- **strftime()**: liefer eine formatierte Zeitangabe aus einem Tupel zurück; kann in Kombination mit `localtime()` für eine aktuelle Zeitangabe benutzt werden
  `time.strftime("%d.%m.%Y %H:%M:%S", time.localtime() v)` 
-  **mktime()**: erzeugt eine Zeitangabe aus einem Tupel
  `time.mktime(tupel)`
- **sleep()**:  haltet das Programm für x Sekunden an
  `sleep(x)`

# Generators
 Generators are used similarly to `range`, but they pause after performing their task and wait until it is called again with `next`. 
 A generator is defined by using `yield`
 ```Python
 def func():
	 task
	 yield x
	 
y = func()
next(y)
 ```

**Generator comprehension**
Generator comprehensions can be used to write one-line generators, by writing
```Python
gen = (x for x in yList)
```