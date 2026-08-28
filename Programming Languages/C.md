https://github.com/codr7/hacktical-c
# Quellcode zu Maschinenprogramm
![[Quellcode zu Maschinenprogramm.png|497x113]]
1. Zuerst werden die Header-Dateien durch den Präcompiler in die  Quellcodedatei eingefügt, das ermöglicht das Einbinden von Standardbibliotheken und fremde Funktionen in das Programm. Die Header-Datei liefert Informationen die an anderer Stelle bereitgestellt werden. Der *Präcompiler* wird über *Direktiven* gesteuert, Befehle die im Quellcode mit dem Zeichen `#` beginnen. 
   >[!note]
   >Der *Präcompiler* fügt die Header Datei in den Quelltext ein und führt weitere Vorbereitungen für den Compiler aus, damit dieser den Quelltext richtig übersetzt.
   >Anweisungen die im Quell text für den Precompiler gedacht sind werden mit `#` gekennzeichnet.
2. Im folgenden Schritt wird der Quellcode in eine Objektdatei übersetzt. Diese sind Maschinenprogramme deren Lage im Speicher des Computers noch durch den *Linker* angepasst werden muss.
3. Im letzten Schritt werden noch weitere Objektdateien mit dem Hauptprogramm verbunden (z.B. weitere Bibliotheken). Das Programm kann jetzt vom Prozessor ausgeführt werden.

# Struktur eines C Programms
![[Struktur C Programm.png]]

## Hallo Welt
```C
#include <stdio.h>
int main(void)
{
	printf("Hallo Welt");
	return 0;
}
```

- mit `#include <stdio.h>` wird die Header Datei oder auch Standardbibliothek `stdio.h` eingefügt die für die Funktion `printf` gebraucht wird
- In der Hauptfunktion `main` werden die auszuführenden Befehle geschrieben, der Parameter `void` kennzeichnet, dass es keinen Übergabewert geben soll
- Nach erfolgreicher Ausführung der Funktion wird der Wert 0 an das OS gegeben, bei Fehlern wird ein Wert != 0 zurückgegeben.

## Kommentare
Kommentare werden mit den Zeichen `/*` begonnen und mit `*/` geschlossen, seit dem C99-Standard kann man Zeilenweise Kommentare mit `//` kennzeichnen.
```C
/* Das ist ein Kommentar*/ printf("Das wird ausgeführt");
// Das ist ein Kommentar für die ganze Zeile printf("Das wird nicht ausgeführt");
```

# Datentypen
## Zeichen

| Datentyp      | Wertebereich | Speichergröße | Anwendung                                                                                                                                                                      |
| ------------- | ------------ | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| char          | 1 Zeichen    | 1 Byte        | Zeichen werden durch einfache Anführungszeichen eingeschlossen. Intern wird das Zeichen als Wert des entsprechenden ASCII-Zeichens gespeichert, z. B. 65 für den Buchstaben a. |
| signed char   | -128 bis 127 | 1 Byte        | Es können auch Ganzzahlen gespeichert werden.                                                                                                                                  |
| unsigned char | 0 bis 255    | 1 Byte        | Es können nur positive Zahlen einschließlich der Null gespeichert werden.                                                                                                      |

## Ganzzahlen

| **Datentyp**           | **Wertebereich**                                                                             | **Speichergröße**    |
| ---------------------- | -------------------------------------------------------------------------------------------- | -------------------- |
| short int              | -32768 bis 32767                                                                             | 2 Byte               |
| unsigned short int     | 0 bis 65535                                                                                  | 2 Byte               |
| int                    | Maschinenabhängig:<br>-32768 bis 32767 (16 Bit)<br>-2,147,483,648 bis 2,147,483,647 (32 Bit) | <br>2 Byte<br>4 Byte |
| unsigned int           | Maschinenabhängig:<br>0 bis 65535 (16 Bit)<br>0 bis 4,294,967,295 (32 Bit)                   | <br>2 Byte<br>4 Byte |
| long int               | -2,147,483,648 bis 2,147,483,647 (32 Bit)                                                    | 4 Byte               |
| unsigned long int      | 0 bis 4,294,967,295 (32 Bit)                                                                 | 4 Byte               |
| long long int          | -9,223,372,036,854,775,808 bis 9,223,372,036,854,775,807 (64 Bit)                            | 8 Byte               |
| unsigned long long int | 0 bis 8,446,744,073,709,551,615 (64 Bit)                                                     | 8 Byte               |
## Gleitkomma Zahlen

| Datentyp    | Wertebereich                           | Genauigkeit                              | Speichergröße                               |
| ----------- | -------------------------------------- | ---------------------------------------- | ------------------------------------------- |
| float       | $1,18*10^{-38}$ bis $3,4*10^{38}$      | 7 Stellen                                | 4 Byte                                      |
| double      | $2,23*10^{-308}$ bis $1,79*10^{308}$   | 15 Stellen                               | 8 Byte                                      |
| long double | $3,37*10^{-4932}$ bis $1,18*10^{4932}$ | 18 bis 33 Stellen<br>(plattformabhängig) | 10 bzw. 12 oder 16 Byte (plattformabhängig) |

## Umwandlung eines Datentyps
Wenn in einer Operation verschiedene Datentypen verwendet werden wird eine *implizite* Typumwandlung nach definierten Regeln durchgeführt.
>[!warning]
>Bei der impliziten Typumwandlung kann es zum Überlauf (z.B. double/int) und Verlust von Nachkommastellen und somit auch zum Verlust von Genauigkeit kommen.

*Explizite* Typumwandlungen können mithilfe von *cast* Anweisungen durchgeführt werden.
```C
int i;
// i wird von int zu double umgewandelt
double (i);

double a, b;
// in x wird das Ergebnis der Ganzzahldivision als double gespeichert
double x = (double) ((int) a) / (int)b)
```

# Variablen
## Definition
Bei der Definition wird einer Variable ein Datentyp, Bezeichner und Wert zugewiesen wird. 
Variablen können nach folgendem Muster definiert werden:
- `Datentyp name;`
- `Datentyp name1, name2;`
- `Datentyp name = ausdruck;`

>[!note]
>`Datentyp name;` ist streng genommen eine *Deklaration*, wobei einer Variablen nur ein Datentyp und ein Bezeichner zugewiesen wird.
>Definitionen sind eigentlich nur eine spezielle Form der Deklaration.

```C
char antwort;
int zahl1, zahl2;
int ergebnis = zahl1 + zahl2
```

Werte werden mit `=` den Variablen zugewiesen:
```C
int zahl = 17; 
```

**Beispiel**
```C
int main(void)
{
	int zahl1 = 3;
	int zahl2 =
	 5;
	int ergebnis = zahl1 + zahl2;
	return 0;
}
```

## Gültigkeitsbereich

**Lokale Variablen**
Lokale Variablen werden innerhalb von Funktionen und Anweisungsblöcken definiert und sind nur in diesen Blöcken gültig, außerhalb des Blockes sind Name und Wert der Variablen unbekannt. 

**Globale Variablen**
Globale Variablen werden außerhalb von Funktionen definiert und sind von ihrer Initialisierung bis zum Ende des Programms gültig. Sie können von allen Funktionen aus gelesen und verändert werden. 
Innerhalb von Funktionen können globale Variablen von lokalen mit gleichem Namen verdeckt werden.

>[!note]
>Die Verwendung von globalen Variablen ist fehleranfällig und sollte möglichst vermieden werden.

**Statische Variablen**
Statische Variablen behalten ihre Lebensdauer über das gesamte Programm und behalten ihre Werte über ihren Gültigkeitsbereich hinweg.
Definiert werden sie mit: `static datenTyp name;`

**Externe Variablen** 
Externe Variablen sind globale Variablen aus externen Dateien oder Bibliotheken. 
Sie werden mit `extern datenTyp name` gekennzeichnet.

# Konstanten 
Konstanten werden für Werte benutzt die sich im Laufe des Programms nicht ändern, etwa physikalische oder andere feste Größen. 
Konstanten werden mit `const` definiert:
```C
const datentyp constName = wert;
```

**Beispiel**
```C
include <stdio.h>
int main(void)
{
	const double pi = 3.14;
	double radius = 14.0;
	
	printf("Der Kreisumfang beträgt: %f.\n", 2*pi*radius);
	getchar();
	return 0;
}
```

>[!note]
>`getchar()` wird benutzt um nach der Ausgabe der Werte auf das drücken der Eingabetaste gewartet, damit die Ausgabe nicht sofort beendet wird.

# Ein- und Ausgabe

## Eingabe
**getchar**
Mit `getchar();` kann die Tastatureingabe von einem Zeichen eingelesen werden, wobei der Rückgabewert eine Zahl ist die dem jeweiligen Zeichen in der [ASCII Zeichentabelle](https://www.ascii-code.com/de) entspricht.
```C
int var = getchar();
```

### scanf
Mit `scanf()` kann man Tastatureingaben abfragen und diese Variablen zuweisen.
Für die Angabe der Variablen werden Platzhalter benutzt.
- int: `%d`, `%i`
- double: `%lf`
- char: `%c`
- Zeichenkette char[]: `%s`

Es ist auch möglich mehrere Werte von der Tastatur einzulesen
```C
scanf("%d, %d, %d", &var1, &var2, &var3);
```

Die Funktion gibt als Rückgabewert die Anzahl der erfolgreich eingelesenen Elemente zurück, damit kann man überprüfen, ob die Eingabe erfolgreich war.
## Ausgabe
**putchar**
Mit `putchar()` kann ein Zeichen auf dem Bildschirm ausgegeben werden. Dabei kann man das Zeichen oder den Zahlenwert aus der ASCII Tabelle übergeben werden.
```C
putchar('a');
putchar(97);
```
 
### printf
`printf()` ermöglicht die formatierte Ausgabe auf den Bildschirm, wobei Variablen durch einen Platzhalter eingefügt werden.
```C
printf("text %var", var);

printf("Die Summe aus %d + %d = %d", num1, num2, num3);
```

#### Formatierung
- Linksbündig: `-`
- alternative Darstellung: `#` 
- Nachkommastellen: `x.yf` (`x` Stellen insgesamt, `y` Nachkommastellen)

#### Steuersequenzen
- `\n`: Zeilenumbruch
- `\a`: Tonausgabe
- `\b`: Schreibmarke wird ein Zeichen nach links gesetzt.
- `\f`: Seitenvorschub
- `\r`: Wagenrücklauf (CR oder Enter)
- `\t`:Tabulator
- `\v`: vertikaler Tabulator
- `\\`: `\` wird im Text ausgegeben
- 
## Übung
Ein Programm das Temperaturangaben con Kelvin (K) in °C umrechnet.
```C
#include <stdio.h>

int main(void)
{
    const double temperaturKelvin = 14.0;
    const double umrechnung = temperaturKelvin - 273.15;

    printf("Die Temperatur in Celsius betraegt: %f.\n", umrechnung);
    getchar();
}
```

# Operatoren
## Arithmetische Operatoren

| **Operation**  | **Operator** | **Code**                             |
| -------------- | ------------ | ------------------------------------ |
| Addition       | `+`          | `summe = summand1 + summand2;`       |
| Subtration     | `-`          | `differenz = minunend - subtrahend;` |
| Multiplikation | `*`          | `produkt = faktor1 * faktor2;`       |
| Division       | `/`          | `quotient = dividend / divisor;`     |
| Modulo         | `%`          | `rest = dividend % divisor;`         |
**Beispiel** 
Addition
```C
#include <stdio.h>
int main(void)
{
	int summand1, summand2, summe;
	summand1 = 18;
	summand2 = 56;
	printf("Addition zweier Zahlen: \n\n");
	printf("Der erste Summand ist a = %d. \n", summand1);
	printf("Der zweite Summand ist b = %d. \n", summand2);
	summe = summand1 + summand2;
	printf("Das Ergebnis ist: %d + %d = %d. \n", summand1, summand2, summe);
	getchar();
	return 0;
}
```

Division mit Rest
```C
#include <studio.h>
int main(void)
{
	int dividend, divisor, quotient, rest;
	dividend = 56;
	divisor = 18;
	printf("\n\nDivision zweier Zahlen:\n\n");
	printf("Der Dividend ist a = %d.\n", dividend);
	printf("Der Divisor ist b = %d.\n", divisor);
	quotient = dividend / divisor;
	printf("Das Ergebnis lautet: %d : %d = %d", dividend, divisor, quotient);
	rest = dividend % divisor;
	printf("Rest: %d\n\n\n", rest);
	getchar();
	return 0;
```

## Relationale Operatoren

| **Operator** | **Code**         | **Wahr, wenn**                 |
| ------------ | ---------------- | ------------------------------ |
| `>`          | `zahl1 > zahl2`  | zahl1 größer als zahl2         |
| `<`          | `zahl1 < zahl2`  | zahl1 kleiner als zahl2        |
| `>=`         | `zahl1 >= zahl2` | zahl1 größer oder gleich zahl2 |
| `<=`         | `zahl1 <= zahl2` | zahl1 kleiner der gleich zahl2 |
| `==`         | `zahl1 == zahl2` | zahl1 gleich zahl2             |
| `!=`         | `zahl1 != zahl2` | zahl1 ungleich zahl2           |
## Logische Operatoren

| **Operator** | **Name**        | **Code**                   | **Wahr, wenn**                                  |
| ------------ | --------------- | -------------------------- | ----------------------------------------------- |
| `&&`         | Logisches UND   | `condition1 && condition2` | condition1 und condition2 sind wahr             |
| \|\|         | Logisches ODER  | condition1 \|\| conditon2  | condition1 oder condition2 oder beide sind wahr |
| `!`          | Logisches NICHT | `!condition`               | condition ist falsch                            |
## Bitoperatoren
Mit Bitoperatoren kann man auf die binäre Darstellung von Zahlen zugreifen und Operationen durchführen.
![[Bitoperatoren.png|554x116]]
![[Bitoperatoren 2.png.png]]

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
# Funktionen

## Aufbau
```C
Typ Name_der_Funktion (Parameter)
{
	Anweisung x;
	return wert;
}

// Beispiel:
int addition (int x, int y)
{
	return x + y;
}
```

## Aufrufen von Funktionen
Funktionen werden durch Angabe des Funktionsnamen und falls nötig mit Zuweisung von Argumenten für die Parameter aufgerufen.

>[!warning]
>Die Anzahl und der Datentyp der Argumente muss mit den Parametern übereinstimmen ansonsten tritt ein Fehler auf.

Sollte die Funktion einen Rückgabewert haben, muss die Funktion einer Variablen zugewiesen werden.

```C
// Aufruf ohne Rückgabewert
Funktionsname(parameter 1, parameter 2);

// Aufruf mit Rückgabewert
var x = Funktionsname(parameter 1, parameter 2) 
```

**Aufruf mit Parametern**
```C
#include <stdio.h>

const double mwst = 0.19;
const double artikel = 5.20;

void add_mwst (double preis)
{
	printf("\n*\t%5.2f EUR\n", preis * (mwst + 1));
}

int main(void)
{
	add_mwst(artikel);
	return 0;
}
```

**Zeiger als Parameter**
Es können auch Zeiger als Argument übergeben werden, dafür muss das Argument als Referenz mit dem Zeichen `&` übergeben werden und der Parameter muss als Zeiger mit dem Zeichen `*` definiert werden. 
```C
#include <stdio.h>

void add(int *zahl1)
{
	zahl1 += 15;
}
int main(void)
{
	int zahl1 = 0;
	add(&zahl);
	return 0;
}
```

## Rückgabe
Funktionen geben Werte mithilfe der `return` Anweisung zurück, wobei mehrere return Anweisungen in einer Funktion stehen können, es kann jedoch immer nur ein Wert zurückgegeben werden.

>[!note]
>Sollte der Datentyp der `return` Anweisung nicht mit dem der Funktion übereinstimmen findet eine implizite Typumwandlung statt. 
>Beispiel: 
>```C
>int rueckgabe()
>{
>	return 2.5
>}
>```
>Es wird statt 2.5 wird 2 zurückgegeben.

**Rückgabe von mehren Werten**
Um mehrere Werte zurückzugeben kann man anstatt der `return` Anweisung, Zeiger oder (globale) Variablen benutzen.

## Funktionsprototypen
Wenn zwei Funktionen sich gegenseitig aufrufen kommt es normalerweise zu einem compile error. Um dies zu umgehen wird *Prototyping* benutzt, wobei eine Funktionsdefinition mit Rückgabewert, Datentyp und Parametern geschrieben.

>[!note]
>Die Trennung von Funktionsdeklaration und Funktionsdefinition können die Prototypen in eine Header Datei auslagern.

Syntax
```C
Rückgabewert FunktionsName (Datentyp var1, Datentyp var2);
```

**Beispiel**
```C
// Prototyp
void ausgabe(int ausgabe);
int add(int num1, int num2)
{
	ausgabe(num1 + num2);
	return(num1 + num2);
}

void ausgabe(int wert)
{
	printf("Die Summe ist %d", wert);
}
```

