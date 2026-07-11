
## Notes
- Bei char in single quotes erwartet C# nur einen Wert 
  z.B. `'b'` aber nicht `'bb'` 

## 1. Datentypen und Variablen
### Variablendeklaration und Initialisierung
Die Deklaration einer Variabel bedeutet, dass man ihr einen Typ und einen Namen zuweist, aber keinen Wert.
```Csharp
int alter;
```

Initialisierung bedeutet, dass einer Variable ein Wert zugewiesen wird (Die Variable muss davor deklariert worden sein):
```Csharp
alter = 87;
```

Man kann Variablen in einem Schritt deklarieren und initialisieren:
```Csharp
int alter = 87;
```

>[!warning]
>Man kann Variablen nur einmal deklarieren, ihre Werte können beliebig oft geändert werden.

**1.)** Finden Sie für die relevanten Kundendaten den passenden Datentyp.
```Csharp 
static void Main(string[] args){
			// int ist für Ganzzahlen (1,2,3,...)
			int myID = 1000;
			// string ist für Zeichenketten ("Hallo", "Ka")
            string vorname = "Alex";
			// double ist für Gleitkommazahlen (2.3, 4.5, 0.1)
            double trainerRating = 4.5;
			
            string email = "test@testest.test";

            double trainingsStunden = 5;

            int besuchteKurse = 8;

            string trainingsziel = "Gains";

            string telefonNummer = "06068986661312";

            string letztesTraining = "12.12.12";
			// Gibt die Variablen auf der Konsole aus
            Console.Write(myID + vorname + trainerRating + email + trainingsStunden + besuchteKurse + trainingsziel);
            Console.Write(telefonNummer + letztesTraining);
```

**2.)** Ergänzen Sie die Beschreibung zu den jeweiligen Code-Abschnitten.

| Code                                        | Beschreibung                                  |
| ------------------------------------------- | --------------------------------------------- |
| `int myNumber;`                             | Deklaration                                   |
| `int myNumber = 10`                         | Deklaration + Initialisierung                 |
| `string myString;`<br>`myString = "Hello";` | Deklaration<br>Initialisierung                |
| `int myNumber = 10;`<br>`myNumber = 20`     | Deklaration + Initialisierung<br>Wertänderung |
### Variablennamen
1. **Bedeutungsvoll**: 
der Name sollte die Funktion/ den Zweck verdeutlichen
z.B `age`, `eingabe`, `ausgabe`, `ergebnis`
2. **Beginnt mit einem Buchstaben oder Unterstrich**
-  der Name muss mit einem Buchstaben oder Unterstrich beginnen
**2.)**
```Csharp
static void Main(string[] args){

            double breite = 20;

            double länge = 30;

            double fläche = breite * länge;

            Console.Write(fläche);
```

**3.)**
```Csharp
static void Main(string[] args){

            double breite = 20;

            double länge = 30;

            double höhe = 4;

            double volumen = breite * länge * höhe;

            Console.Write(volumen + " m^3");
```

**4.)**
```Csharp
static void Main(string[] args){

            double breite = 20;

            double länge = 30;

            double höhe = 4;

            double umfang = (2 * breite) + (2 * länge);

            string str = $"Der Umfang der Fläche ist {umfang} m";

            Console.Write(str);
```

**5.)**
```Csharp
static void Main(string[] args){
			// escape character \n erzeugt einen Zeilenumbruch
            string nachricht ="Hallo liebes Mitglied,\n leider warst du heute nicht da.\n Das nächste Training ist am 9.9.99.\n Bei Fragen melden Sie sich bitte nicht";

            Console.Write(nachricht);
```

### Änderung des Datentyps
Um Daten von einem Typ in einen anderen umzuwandeln (Typecast), benutzen wir die Funktion `Convert.To...`:
```Csharp
int myInt = 10;
double myDouble = 5.25
bool myBool = true;

Console.WriteLine(Convert.ToString(myInt));
Console.WriteLine(Convert.ToDouble(myInt));
Console.WriteLine(Convert.ToInt32(myDouble));
Console.WriteLine(Convert.ToString(myBool));
Console.WriteLine(Convert.ToBoolean("True"));
```
### 2. Vertiefung: Datentypen und Variablen
**1.)**
```Csharp
static void Main(string[] args){

            // Preis in Euro

            // Gewicht in Gramm

            double packungGewicht1 = 350;

            double packungPreis1 = 0.99;

            double packungGewicht2 = 950;
			// Runded den Wert 
            double packungPreis2 = Math.Round((0.99 / 350) * 950, 2);

            string text = $"Der Preis der ersteb Packung ist {packungPreis1}€, der Preis der zweiten ist {packungPreis2}€";

            Console.WriteLine(text);
```

**2.)**
```Csharp
static void Main(string[] args){

            int var1 = 2000000000;

            int var2 = 2000000000;

            Console.Write(var1+var2);

            // Das Ergebnis ist -294967296, da es zu einem Überlauf kam.

            // Der höchste Wert wurde überschritten und deswegen beginnt es am untersten Wert
```

**3.)**
```Csharp
static void Main(string[] args){

            // Wähle die richtigen Datentypen aus

            int alter = 3;

            double Kontostand = 20.01;

            char wochentag = '3';

            string name = "Darf";

            bool verheiratet = true;

            string text = $" Alter: {alter}\n Kontostand: {Kontostand}\n Wochentag: {wochentag}\n Name: {name}\n Verheiratet: {verheiratet}";

  

            Console.Write(text);
```

**4.)**
```Csharp
static void Main(string[] args){

            // Berechne eine double mit einer int Zahl und speichere

            // wähle einen geeigneten Datentyp für das Ergebnis

            // gib das Ergebnis mit der str aus

            int zahl1 = 1;

            double zahl2 = 3.4;

            string test = "hallo welt";

  

            double erg = zahl1 + zahl2;

            Console.Write(test + " " + erg);
```

## Eingabe / Ausgabe

### 4. Eingabe
**Eingabe**
Um Eingaben von Usern zu erfassen benutzen wir die Funktion `Console.ReadLine()`.
```Csharp
Console.Write("Bitte Namen eingeben: ");
string Name = Console.ReadLine();
Console.Write($"Hallo {name}")
```
### 5.Übungen EVA
```Csharp
 static void Main(string[] args){

           Console.WriteLine("Geben Sie ihr Gewicht ein");

           double gewicht = Convert.ToDouble(Console.ReadLine());

           Console.WriteLine("Geben Sie Größe ein");

           double groeße = Convert.ToDouble(Console.ReadLine());

            double bmi = Math.Round(gewicht / (groeße * groeße), 2);

            Console.WriteLine($"Bei einem Gewicht von {gewicht} kg und einer Größe von {groeße} m ist der BMI {bmi}");

  

        }
```

```Csharp
static void Main(string[] args){

          Console.WriteLine("Geben sie ihr alter an");

          double alter = Convert.ToDouble(Console.ReadLine());

          alter = 220 - alter;

          Console.WriteLine($"Die maxinale Herzfrequenz beträgt {alter}");
        }
```

```Csharp
 static void Main(string[] args){

            Console.WriteLine("Geben Sie ihren aktivitätsFktor an:");

            Console.WriteLine("Wenig keine Bewegeung:\t 1.3\n leicht Aktiv:\t 1.375\n moderat Aktiv:\t 1.55\n Sehr aktiv:\t 1.725");

            decimal faktor = Convert.ToDecimal(Console.ReadLine());

            decimal bedarf = (2250m * faktor) / 10;

            Console.WriteLine($"Ihr Kalorienbedarf beträgt {bedarf} kcal");

        }
      
```

### 6. VT Übungen EVA
```Csharp
 static void Main(string[] args){

            Console.WriteLine("Name angeben");
            string name = Console.ReadLine();

            Console.WriteLine("alter angeben");
            int alter = Convert.ToInt32(Console.ReadLine());
            
            Console.WriteLine("Verheiratet?");
            bool verheiratet = Convert.ToBoolean(Console.ReadLine());
            
            Console.WriteLine($"{name}\n{alter}\n{verheiratet}");
        }
```

```Csharp
   static void Main(string[] args){

            Console.WriteLine("Mathematische Berechnungen\nBitte geben Sie eine Zahl ein");

            double zahl1 = Convert.ToDouble(Console.ReadLine());

            Console.WriteLine("Geben Sie eine 2. Zahl ein");

            double zahl2 = Convert.ToDouble(Console.ReadLine());

            Console.WriteLine($"Es wurden folgende Zahlen eingegeben; {zahl1}\t {zahl2}");

            Console.WriteLine("Ergebnis für Addition:\t\t" + (zahl1 + zahl2));

            Console.WriteLine("Ergebnis für Subtraktion:\t" + (zahl1 - zahl2));

            Console.WriteLine("ERgebnis für Multiplikation:\t" + (zahl1 * zahl2));

            Console.WriteLine("ERgbnis für Division:\t\t" + (zahl1 / zahl2));
```

```Csharp
static void Main(string[] args){

           Console.WriteLine("Beispiel für Escape:\n\nEinsatz von tab und new line\n\ntext\ttext\ttext\ntext\ttext\ttext\n\n Ausgabe eines Pfades: \"C:\\Programme\\Visual");

        }
```

## (7.) Operatoren
### Arithmetische Operatoren
Diese Operatoren werden für arithmetische (mathematische) Operationen benutzt:

| Operator | Bedeutung      | Beispiel             | Ergebnis |
| :------: | -------------- | -------------------- | :------: |
|    +     | Addition       | int i1 = 3+2         |    5     |
|    -     | Subtraktion    | int i2 = 3-2         |    1     |
|    *     | Multiplikation | int i3 = 3\*2        |    6     |
|    /     | Division       | int i4 = 6 / 3       |    2     |
|    %     | Modulo         | int i5 = 10 % 5      |    0     |
|    ++    | Inkrement      | int i6 = 5;<br>i6++; |    6     |
|    --    | Dekrement      | int i7 = 5;<br>i7--; |    4     |
### Zuweisungsoperatoren
Diese werden bei der Zuweisung von Variablen und Werten benutzt. Auch werden sie bei Wiederzuweisung nach arithmetischen Operationen benutzt.

| Operator | Bedeutung                | Beispiel     | Analog zu        |
| :------: | ------------------------ | ------------ | ---------------- |
|    =     | Zuweisung                | int i1 = 3   |                  |
|    +=    | Additionszuweisung       | int i2 += 3  | int i2 = i2 + 3  |
|    -=    | Subtraktionszuweisung    | int i3 -= 3  | int i3 = i3 - 3  |
|   \*=    | Multiplikationszuweisung | int i4 \*= 3 | int i4 = i4 \* 3 |
|    /=    | Divisionszuweisung       | int i5 /= 3  | int i5 = i5 / 3  |
|    %=    | Modulozuweisung          | int i6 %= 3  | int i6 = i6 % 3  |
### Vergleichsoperatoren
Diese Operatoren werden benutzt um Werte zu vergleichen.

| Operator | Bedeutung      | Beispiel      | Ergebnis |
| :------: | -------------- | ------------- | -------- |
|    ==    | Gleich         | if (5 \== 5)  | true     |
|    !=    | Ungleich       | if (5 != 7)   | true     |
|    <     | Kleiner        | if (7 < 5)    | false    |
|    >     | Größer         | if (7 > 5)    | true     |
|    <=    | Kleiner-Gleich | if (10 <= 10) | true     |
|    >=    | Größer-Gleich  | if (5 >= 8)   | false    |
### Logische Operatoren
Mit diesen Operatoren kann man Konditionen verketten und die Steuerungsstruktur optimieren.
```Csharp
bool a = true;
bool b = false;
```

|   Operator   | Bedeutung             | Beispiel      | Ergebnis |
| :----------: | --------------------- | ------------- | -------- |
|  && oder &   | Logisches UND         | if (a && b)   | false    |
| \|\| oder \| | Logisches ODER        | if (a \|\| b) | true     |
|      !       | Logisches NICHT       | if (!a)       | false    |
|      ^       | Exklusives ODER (XOR) | if (a^b)      | true     |
>[!info] XOR
>XOR prüft ob a oder b wahr ist, wenn beide `true` oder `false` sind ist XOR `false`.
>

### (8.) Übungen
**1.)**
144 % 7 = 4
123456 % 100 = 56
121 % 11 = 0
10 % 5 = 0
11 % 2 = 1

**2.)**
x = 13

x += 12; x = 25
x \*= 12; x = 156
x = ++x; x =14
x = x++; x = 14

**3.)**
x1 = true; x2 = false
a) ergebnis = (x1 && x2)
b) ergebnis = !(x1 || x2)
c) ergebnis = (!x1 && !x2)
d) ergebnis = (x1 || x2) && (!x1 && x1)

**4.)**
![[Wahrheitstabelle11.11.24.png]]

### (9.) Praktische Übungen
**1.)**
```Csharp
static void Main(string[] args) {

	Console.WriteLine("Gebe Zahl1 ein.");
    double zahl1 = Convert.ToDouble(Console.ReadLine());
    Console.WriteLine("Gebe Zahl1 ein.");
    double zahl2 = Convert.ToDouble(Console.ReadLine());
    Console.WriteLine($"{zahl1} + {zahl2} = {zahl1 +zahl2}");
    Console.WriteLine($"{zahl1} - {zahl2} = {zahl1 -zahl2}");
    Console.WriteLine($"{zahl1} * {zahl2} = {zahl1 *zahl2}");
    Console.WriteLine($"{zahl1} / {zahl2} = {zahl1 /zahl2}");
   Console.WriteLine($"{zahl1} % {zahl2} = {zahl1 %zahl2}");
   
}
```

**2.)**
```Csharp
static void Main(string[] args) {

	Console.WriteLine("Geben Sie ihre Geschwindigkeit in Km/h als ganze Zahl an");
	int geschwindigkeit = Convert.ToInt32(Console.ReadLine());
	Console.WriteLine($"Der Mindestabstand zu dem Fahrzeug vor ihnen sollte {geschwindigkeit / 2} m betragen.);

// 2b
	double reaktionsweg = geschwindigkeit * 3 / 10;
	int bremsweg = (geschwindigkeit / 10) * (geschwindigkeit / 10);
	Console.WriteLine($"Der Anhalteweg beträgt {reaktionsweg + bremsweg} m.");

```

## Verzweigung
### If Statment
In C# können Verzweigungen mit dem `if` Statement ermöglicht werden.
```Csharp
if (Bedingung) {
	Anweisung
}
else {
	Alternative Anweisung
}
```

Die Bedingung ist ein boolscher Wert, der `true` oder `false` sein kann.
```Csharp
if (frühstück) {
	Console.WriteLine("Es gab Frühstück")
}
else {
	Console.WriteLine("Du gehst hungrig zur Schule")
}
```

Man kann auch Vergleichsoperatoren in der Bedingung benutzen.
```Csharp
int x = 5;
int y = 3;
if (x < 8 && y > 2) {
	Console.WriteLine("x ist kleiner als 8 und y ist größer als 2" )
}
```

`if` Statements können auch verschachtelt werden.
```Csharp
if(bedingung) {
	if(bedingung2){
		anweisung
	}
	else {
		anweisung
	}
}
else{
	alternative anweisung
}
```

Auch können mehrere Verzweigungen mit `else if` ermöglicht werden.
```Csharp
if (bedingung1) {
	anweisung1
}
else if (bedingung2) {
	anweisung2
}
else {
	alternative anweisung
}
```

### Aufgaben if-Statements
**1.** Schreibe ein Programm das den Benutzer fragt ob es Regnet.
```Csharp
static void Main(string[] args)
        {
           Console.WriteLine("Regnet es?");
           string regen = Console.ReadLine();
           if (regen == "ja") {
                Console.WriteLine("Nimm einen Regenschirm mit");
           }
           else {
                Console.WriteLine("Viel Spaß im trockenen");
           }
        }
```

**2.** Schreib ein Programm das Berechnet ob ein angegebenes Jahr ein Schaltjahr ist.
```Csharp
 static void Main(string[] args)
        {
           Console.WriteLine("Gib eine Jahreszahl ein");
           int jahreszahl = Convert.ToInt32(Console.ReadLine());
           if (jahreszahl % 2 == 0 && jahreszahl % 100 != 0) {
            Console.WriteLine($"{jahreszahl} ist ein Schaltjahr");
           }
           else if (jahreszahl % 400 == 0) {
            Console.WriteLine($"{jahreszahl} ist ein Schaltjahr");
           }
           else {
            Console.WriteLine($"{jahreszahl} ist kein Schaltjahr");
           }
        }
```

**3.** Schreibe ein Programm das eine eingegebene Punktzahl auswertet.
```Csharp
static void Main(string[] args)
        {
            Console.WriteLine("Gib eine Punktezahl ein");
            int punktezahl = Convert.ToInt32(Console.ReadLine());
            if (punktezahl <= 100 && punktezahl >= 90){
                Console.WriteLine("Sehr gut");
            }
            else if (punktezahl < 90 && punktezahl >= 75) {
                Console.WriteLine("Gut");
            }
            else if (punktezahl < 75 && punktezahl >= 60) {
                Console.WriteLine("Befriedigend");
            }
            else if (punktezahl < 60 && punktezahl >= 45){
                Console.WriteLine("Ausreichend");
            }
            else {
                Console.WriteLine("Nicht bestanden");
            }
        }
```

**4.** Schreib ein Programm das einen Wochentag und eine Anzahl von Tagen erfragt und dann ausgibt welcher Tag nach der eingegebenen Anzahl ist.
```Csharp
static void Main(string[] args)

        {
           string[] tage = new string[7] {"Montag", "Dienstag", "Mittwoch", "Donnerstag", "Freitag", "Samstag", "Sonntag"};
           int zugriffIndex = 0;
           
           Console.WriteLine("Gib einen Wochentag ein");
           string tag = Console.ReadLine();
           
           Console.WriteLine("Gibt eine Anzahl von Tagen ein");
           int anzahlTage = Convert.ToInt32(Console.ReadLine());
           
           if (tag == "Montag"){
                zugriffIndex = 0;
           }
           else if (tag == "Dienstag") {
                zugriffIndex = 1;
           }
           else if (tag == "Mittwoch") {
                zugriffIndex = 2;
           }
           else if (tag == "Donnerstag") {
                zugriffIndex = 3;
           }
           else if (tag == "Freitag") {
                zugriffIndex = 4;
           }
           else if (tag == "Samstag") {
                zugriffIndex = 5;
           }
           else if (tag == "Sonntag") {
                zugriffIndex = 6;
           }
            zugriffIndex = zugriffIndex + (anzahlTage % 7);
           Console.WriteLine($"Heute ist {tag}, in {anzahlTage} ist {tage[zugriffIndex]}");
        }
```

**5.** Schreib ein Programm das den Preis eines Tickets berechnet.
```Csharp
static void Main(string[] args)

        {
          Console.WriteLine("Geben Sie ihr Alter an");
          int alter = Convert.ToInt32(Console.ReadLine());
          
          Console.WriteLine("Ist heute ein Sondertag?");
          string sondertag = Console.ReadLine();
          bool sondertagBool;
          if( sondertag == "Ja"){
               sondertagBool = true;
          }    
          else {
               sondertagBool = false;
          }

          int eintritt = 0;
          int preis;

          if(alter <= 6){
               eintritt=0;
          }
          else if(alter <= 18){
               eintritt = 8;
          }
          else if(alter > 18 && alter < 65){
               eintritt = 12;
          }
          else if(alter >= 65){
               eintritt = 6;
          }
          
         if(sondertagBool){
               Console.WriteLine($"Der Preis beträft {eintritt/2}€");
         }
         else{
          Console.WriteLine($"Der Eintritt beträgt {eintritt}€");
         }
     }
```
### Pair Programming
```Csharp
static void Main(string[] args)

        {
            Console.WriteLine("Wie viele Schrauben");
            int schrauben = Convert.ToInt32(Console.ReadLine());
            
            Console.WriteLine("Wie viele Muttern");
            int muttern = Convert.ToInt32(Console.ReadLine());
            
            Console.WriteLine("Wie viele Unterlegsscheiben");
            int unterlegsscheiben = Convert.ToInt32(Console.ReadLine());
            
            int preisSchrauben = schrauben * 5;
            int preisMutter = muttern * 3;
            int unterlegsscheibenpreis = unterlegsscheiben * 1;
            
            if(schrauben != muttern){
                Console.WriteLine("Kontrollieren sie ihre Bestellung!!!!!!!");
            }
            else{
                Console.WriteLine("Die Bestellung passt");
            }
            Console.WriteLine($"Der gesamtpreis ist {preisSchrauben + preisMutter + unterlegsscheibenpreis} ct");
        }
```

```Csharp
static void Main(string[] args)

        {
            Console.WriteLine("Wie hoch ist der Preis?");
            double preis = Convert.ToDouble(Console.ReadLine());
            if (preis < 100)
            {
                double kosten = preis + 5;
                Console.WriteLine("Die Kosten sind " + kosten);
            }
            else if (preis >= 100 && preis <= 200)
            {
                double kosten = preis + 2;
                Console.WriteLine("Die Kosten sind " + kosten);
            }
            else
            {
                Console.WriteLine("Die Kosten sind " + preis);
            }
        }
```

## For Schleife
**1.)**
Schreibe ein Programm das 5 Zahlen aufnimmt und die größte ermittelt und ausgiebt.
```Csharp
 static void Main(string[] args)
          {
               int groessteZahl = 0;
               int kleinsteZahl;
               int[] array = new int[5];
               for(int i = 0; i < 5; i++){
                    Console.WriteLine($"Gib Zahl Nr.{i+1} an");
                    array[i] = Convert.ToInt32(Console.ReadLine());
                    Console.WriteLine($"Array Platz {i+1} ist {array[i]}");
               }
               groessteZahl =array[0];
               for(int x = 0; x < array.Length-1; x++){
                    if(array[x+1]>array[x]){
                         groessteZahl = array[x+1];
                    }
               }
               kleinsteZahl = array[0];
               for(int y = 0; y < array.Length-1; y++){
                    if(array[y+1]<array[y]){
                         kleinsteZahl = array[y+1];
                    }
               }
               Console.WriteLine($"Die größte Zahl ist {groessteZahl}\n Die kleinste Zahl ist {kleinsteZahl}");
          }
```

**2.)**
Schreibe ein FizzBuzz Programm.
```Csharp
static void Main(string[] args)
          {
               for(int i = 1; i<=100; i++){
                    if(i % 3 == 0){
                         Console.WriteLine("Fizz");
                    }
                    else if(i % 5 == 0){
                         Console.WriteLine("Buzz");
                    }
                    else if(i % 5 == 0 && i % 3 == 0){
                         Console.WriteLine("FizzBuzz");
                    }
                    else {
                         Console.WriteLine(i);
                    }
               }
          }
```
**3.)**
Schreibe ein Programm das den besten Lieferservice aufgrund von einigen Eigenschaften auswählt

## While-Schleife
Die Syntax für eine `while` Schleife ist:
```Csharp
while(bedingung) {
Anweisung
}
```

Ein Beispiel ist:
```Csharp
int i = 10;
while (i<15) {
	Console.WriteLine("Eine Zahl: " + i);
	i++;
}
```

### Übungen
**1.)** Schreibe ein Programm, das mit einer While-Schleife Zahlen von 1 an aufsummiert, bis die Summe 100 oder mehr erreicht. Gib dann die Summe und die Anzahl der addierten Zahlen aus.
```Csharp
static void Main(string[] args)
{
	int summe = 0;
	int anzahl = 0;
	int zahl = 0;
	while (summe < 100){
		zahl +=1;
		summe += zahl;
		anzahl += 1;
	}
	Console.WriteLine($"Die Summe ist {summe} und es wurden {anzahl} Zahlen addiert")
}
```

**2.)** Schreibe ein Programm, das den Benutzer auffordert, eine Zahl zwischen 1 und 10 einzugeben. Wenn die Eingabe außerhalb dieses Bereichs liegt, soll die Schleife den Benutzer erneut fragen.
```Csharp
static void Main(string[] args){
	Console.WriteLine("Gibt eine Zahl zwischen 1 und 10 ein");
	int i = Convert.ToInt32(Console.ReadLine());
	while ( i < 1 || i > 10){
		Console.WriteLine("Die Zahl ist ungültig. Gib eine andere an.")
		i = Convert.ToInt32(Console.ReadLine());
	}
	Console.WriteLine($"Die Zahl ist {i});
}
```

**3.)** 
Schreibe ein Program, bei dem der Benutzer eine zufällig generierte Zahl zwischen 1 und 100 raten muss. Das Program sagt ob die Eingabe zu hoch, zu niedrig oder korrekt ist, bis die Zahl richtig geraten wurde.
```Csharp
static void Main(string[] args) {
	Random random = new Random();
	int zufallszahl = random.Next(1, 100);
	Console.WriteLine("Rate die Zahl");
	int rateVersuch = Convert.ToInt(Console.ReadLine());
	while(rateVersuch = Convert.ToInt32(Console.ReadLine());
		if(rateVersuch < zufallszahl){
			Console.WriteLine("Die Zahl ist zu niedrig. Versuche es erneut.)
		}
		else if(rateVersuch > zufallszahl){
		
		}
}
```
# Zufallszahlen

# Arrays
**AB**
```Csharp
static void Main(string[] args){
            string weiter;
            char[] arr = {'1','2','3','4','5','6','7','8'};
            
            do{
            Console.WriteLine("Welche Sitze wollen sie belegen?");
            for(int i = 0; i < arr.Length; i++){
            Console.Write($"[{arr[i]}] ");
            }
            Console.WriteLine("");

            int platzauswahl = Convert.ToInt32(Console.ReadLine()) - 1;

            arr[platzauswahl] = 'X';

            for(int i = 0; i < arr.Length; i++){
            Console.Write($"[{arr[i]}] ");
            }

            Console.WriteLine("");
            Console.WriteLine("Möchten sie weitere Plätze buchen? \nJ/N");
            weiter = Console.ReadLine();

            } while(weiter != "N");
        }
```

## 2-Dimensionales Array
```Csharp
static void Main(string[] args){
            string weiter;

            string[,] arr = {{"01","02","03","04","05","06","07","08"}, {"11","12","13","14","15","16","17","18"}};

            // Ausgabe

            Console.WriteLine("Sitzplätze");

            for(int k = 0; k< arr.GetLength(0); k++){

                for(int i = 0; i < arr.GetLength(1); i++) {

                    Console.Write($"[{arr[k,i]}]");

                }

                Console.WriteLine();

            }

            do{

            // Eingabe

            Console.WriteLine("Wählen Sie die Reihe aus");

            int reiheauswahl = Convert.ToInt32(Console.ReadLine())-1;

            Console.WriteLine("Welche Sitze wollen sie belegen?");

            int platzauswahl = Convert.ToInt32(Console.ReadLine()) - 1;

  

            arr[reiheauswahl,platzauswahl] = "X";

            Console.WriteLine("Sitzplätze");

            for(int k = 0; k< arr.GetLength(0); k++){

                for(int i = 0; i < arr.GetLength(1); i++) {

                    Console.Write($"[{arr[k,i]}]");

                }

                Console.WriteLine();

            }

  

            Console.WriteLine("Möchten sie weitere Plätze buchen? \nJ/N");

            weiter = Console.ReadLine();

            } while(weiter == "J");

        }
```

**Minesweeper**
```Csharp
static void Main(string[] args)
        {
            char[,] spielfeld = {
                {'.','.','*', '.', '.' },
                {'.','.','*', '.', '.'},
                {'.','.','*', '.', '.'},
                {'.','.','*', '.', '.'},
                {'.','.','*', '.', '.'}
            };

            string weiter = "j";
            
            do{
            
            for (int i = 0; i < spielfeld.GetLength(0); i++)
            {
                for (int j = 0; j < spielfeld.GetLength(1); j++)
                {
                    Console.Write(spielfeld[i, j] + " ");
                }
                Console.WriteLine();
            }

            int anzahlMinen = 0;
            for (int i = 0; i < spielfeld.GetLength(0); i++)
            {
                for (int j = 0; j < spielfeld.GetLength(1); j++)
                {
                    if(spielfeld[i, j] == '*'){
                        anzahlMinen++;
                    }
                }
            }
            Console.WriteLine($"Es gibt {anzahlMinen} Minen");

            Console.WriteLine("Wähle eine Zeile aus");
            int zeile = Convert.ToInt32(Console.ReadLine());

            Console.WriteLine("Wähle eine Spalte aus");
            int spalte = Convert.ToInt32(Console.ReadLine());

            if(spielfeld[zeile,spalte] == '.') {
                spielfeld[zeile,spalte] = '*';
            }
            else{
                spielfeld[zeile,spalte] = '.';
            }
            Console.WriteLine("Weiter j/n");
            weiter = Console.ReadLine();
            }while(weiter == "j");
        }
```


# Aufgabe TicTacToe
```Csharp
 // Funktion zur Ausgabe des Spielfeldes    
        static void Ausgabe(char[,] spielfeld)
        {
            for (int i = 0; i < spielfeld.GetLength(0); i++)
            {
                Console.Write("| ");
                for (int j = 0; j < spielfeld.GetLength(1); j++)
                {
                    Console.Write(spielfeld[i, j] + " | ");
                }
                Console.WriteLine();
            }
        } 

        static void Main(string[] args)
        {
            // Der Spieler wird über die Runde bestimmt;
            // ungerade Runde => Sp1, gerade Runde => Sp2
            int runde = 1;

            // Spieler und Zeichen werden in den Variablen gespeichert
            int spieler;
            char spielerSymbol;

            // Spielende wird durch die Anzahl von freien Feldern (0) oder
            // einem Gewinner festgelegt
            int freieFelder = 9;
            int spielGewonnen = 0;

            // Erstellen des Spielfeldes
            char[,] spielfeld = {
                {'*','*','*'},
                {'*','*','*'},
                {'*','*','*'},
            };

            // Ausgabe Funktion wird aufgerufen
            Ausgabe(spielfeld);

            // do while Schleife
            do
            {
                // Spieler wird bestimmt
                if (runde % 2 != 0)
                {
                    spieler = 1;
                   spielerSymbol = 'X';
               }
               else
                {
                   spieler = 2;
                    spielerSymbol = 'O';
                }

                int eingabeUeberprüfen = 1;
                while (eingabeUeberprüfen == 1)
                {
                    // try-catch zum Auffangen von Fehlern
                    try{
                    // Eingabeaufforderung an den aktuellen Spieler
                    Console.WriteLine($" Spieler {spieler}, wo wollen Sie ihr Zeichen setzen?");
  
                    Console.WriteLine("Zeile (1-3):");
                    int auswahlZeile = Convert.ToInt32(Console.ReadLine()) - 1;   

                    Console.WriteLine("Spalte (1-3):");
                    int auswahlSpalte = Convert.ToInt32(Console.ReadLine()) - 1;

                    // Überprüfen ob das ausgewählte Feld schon ein Spielersymbol enthält
                    if (spielfeld[auswahlZeile, auswahlSpalte] != '*')
                    {
                        Console.WriteLine("Dieses Feld ist schon belegt.");
                    }
                    else
                    {
                        // Spielersymbol wird "eingetragen"
                        spielfeld[auswahlZeile, auswahlSpalte] = spielerSymbol;
                        eingabeUeberprüfen = 0;
                    }
                    }
                    catch(Exception e){
                        Console.WriteLine("Es ist ein Fehler aufgetreten.");
                    }
                }

                Ausgabe(spielfeld);

                // Es wird überprüft ob es eine 3er Reihe gibt
                for (int i = 0; i <= 2; i++)
                {
                    if (spielfeld[i, 0] == spielerSymbol && spielfeld[i, 1] == spielerSymbol && spielfeld[i, 2] == spielerSymbol)
                    {
                        Console.WriteLine($"Spieler {spieler} hast gewonnen");
                        spielGewonnen = 1;
                    }
                }

                for (int i = 0; i <= 2; i++)
                {
                    if (spielfeld[0, i] == spielerSymbol && spielfeld[1, i] == spielerSymbol && spielfeld[2, i] == spielerSymbol)
                    {
                        Console.WriteLine($"Spieler {spieler} hast gewonnen");
                        spielGewonnen = 1;
                    }
                }


                if (spielfeld[0, 0] == spielerSymbol && spielfeld[1, 1] == spielerSymbol && spielfeld[2, 2] == spielerSymbol)
                {
                    Console.WriteLine($"Spieler {spieler} hast gewonnen");
                    spielGewonnen = 1;
                }


                else if (spielfeld[0, 2] == spielerSymbol && spielfeld[1, 1] == spielerSymbol && spielfeld[2, 0] == spielerSymbol)
                {
                    Console.WriteLine($"Spieler {spieler} hast gewonnen");
                    spielGewonnen = 1;
                }

                // Runde wird erhöht um den Spieler zu wechseln
                // Anzahl der freien Felder wird reduziert
                runde++;
                freieFelder--;

                // Es wird überprüft ob es einen Gewinner oder keine freien Felder mehr gibt
            } while (freieFelder != 0 || spielGewonnen != 1);

            Console.WriteLine("Game Over.");
        }
```

# OOP

>[!note] Begriffe
>- *OOA*: Objektorientierte Analyse
>  Analyse des Problems
>- *OOD*: Objektorientiertes Design
>  Aufteilung des Problems in Klassen
>- *OOP*: Objektorientierte Programmierung
>  Erstellen der Lösungen
>  
> - *Prozedurale Programmierung*
>   Daten und Funktionen, welche diese verändern sind getrennt.
>   procedures or methods perform operations on data
> - OOP:
>   Daten und Methoden, welche diese verändern können, bilden eine Einheit
>   creating objects that contain both data and methods

**Vorteile**
- OOP ist schneller und einfacher zum Ausführen
- OOP bietet eine klare Struktur für die Programme
- OOP hilft dabei Wiederholungen zu vermeiden
- ermöglicht es wiederverwendbare Applikationen mit weniger Code und kürzerer Entwicklungsdauer zu erstellen

## Klassen und Objekte
Klassen sind "Blaupausen" oder abstrakte Gebilde und Objekte sind Instanzen von Klassen.
z.B.:
- **Klasse**: Frucht
  **Objekte**: Apfel, Banane, Mango
- **Klasse**: Auto
  **Objekte**: Volvo, Audi, Toyota

Eine Klasse besitzt *Attribute* die Eigenschaften beschreiben, wie Gewicht oder Farbe, und *Methoden*, durch diese kann die Klasse handeln, wie etwa fahren oder bremsen.
### Klassen erstellen
Um eine Klasse zu erstellen benutzen wir den Begriff `class`
```CSharp
class Car
{
	string color = "red"
}
```

>[!note]
>Es ist best-practice den Klassennamen groß zu schreiben.

Es kann eine eigene Klasse "Programm" in einer eigenen Datei erstellt werden, diese beinhaltet den Programmcode der ausgeführt werden soll.
```Csharp
class Programm
{
	static void Main(string[] args)
     {
	     # Programmcode
     }
}
```
### Objekte erstellen
Um Objekte zu erstellen benutzt man eine Klasse und instanziert ein Objekt.
```Csharp
static void Main(string[] args)
{
	car myCar = new Car();
	Console.WriteLine(myCar.color)
}
```

Es können auch mehrere Objekte erstellt werden
```Csharp
class Car
{
	string color = "red";
	
	static void Main(string[] args)
	{
		Car myCar1 = new Car();
		Car myCar2 = new Car();
	}
}
```

### Class Members
Attribute und Methoden werden auch als Class Members bezeichnet.
Um auf Attribute zuzugreifen benutzt man `Objekt.Attribut`
```Csharp
Car myCar = new Car();
Console.WriteLine(MyCar.color);
```

### Methoden
Methoden werden benutzt damit das Objekt Handlungen ausführen kann.
```Csharp
public void vollGas()
{
	Console.WriteLint("Das Auto fährt so schnell es kann");
}
```

Methoden werden ähnlich wie Attribute aufgerufen: `Objekt.Methode()`
```Csharp
myCar.vollGas();
```

### Zwischen Beispiel

`Auto.cs` Datei
```Csharp
class Auto
{
	string model;
	string color;
	int year;
	
	public void vollGas()
	{
		Console.WriteLine("Das Auto fährt ganz schnell");
	}
}
```

`programm.cs`
```Csharp
class Program
{
	static void Main(string[] args)
	{
		Auto Ford = new Auto();
		Ford.model = "Mustang";
		Ford.color = "red";
		Ford.year = 1969;
	
		Auto Opel = new Auto();
		Opel.model = "Astra";
		Opel.color = "white";
		Opel.year = 2005;
		
		Console.WriteLine(Ford.model);
		Console.WriteLine(Opel.color);
	}
}
```

### Konstruktor
Ein Konstruktor ist eine spezielle Methode die benutzt wird um Objekte zu initialisieren und initiale Werte zu definieren.
```Csharp
// Create a class
class Car
{
	public string model;
	
	public Car()
	{
		model = "mustang"
	}
	
	static void Main(string[] args)
	{
		Car Ford = new Car();
		// the output will display "Mustang"
		Console.WriteLine(ford.model);
	}
}
```

Ein Konstruktor kann auch Parameter benutzen die beim initialisieren des Objekts übergeben werden.
```Csharp
class Car
{
	public string model;
	
	public Car(string modelName)
	{
		model = modelName;
	}
	
	static void Main(string[] args)
	{
		Car Ford = new Car("Mustang");
		Console.WriteLine(Ford.model);
	}
}
```

Es können auch mehrere Parameter definiert werden
```Csharp
class Car
{
	public string model;
	public string color;
	public int year;
	
	// Create a class constructor
	public Car(string modelName, string modelColor, int modelYear)
	{
		model = modelName;
		color = modelColor;
		year = modelYear;
	}
	
	static void Main(string[] args)
	{
		Car Ford = new Car("Mustang", "Red", 1969);
		Console.WriteLine($"{Ford.color}, {Ford.year}, {Ford.model}");
	}
}
```

### Access Modifiers
Access modifiers werden benutzt um den Zugriff und die Sichtbarkeit auf die Klasseninhalte einzustellen.

| Modifier    | Description                                                                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `public`    | The code is accessible for all classes                                                                                                                  |
| `private`   | The code is only accessible within the same class                                                                                                       |
| `protected` | The code is accessible within the same class, or in a class that is inherited from that class. You will learn more about inheritance in a later chapter |
| `internal`  | The code is only accessible within its own assembly, but not from another assembly. You will learn more about this in a later chapter                   |
Wenn ein Inhalt mit `private` modifiziert wurde, kann nur von innerhalb der selben Klasse zugegriffen werden. Dies wird benutzt um sensible Inhalte von unbefugten fernzuhalten.
```Csharp
class Car
{
	private string model = "Mustang"
	
	static void Main(string[] args)
	{
		Car myObj = new Car();
		// Der ouput wird "Mustang" anzeigen
		Console.WriteLine(myObj.model)
	}
}

class Program
{
	static void Main(string[] args)
	{
		Car myObj = new Car();
		// Der output wird einen Fehler anzeigen, da Zugriff nur von innerhalb der Klasse Car erlaubt ist
		Console.WriteLine(myObj.model);
	}
}
```

Wenn ein Inhalt mit `public` modifiziert ist, kann von jeder Klasse aus darauf zugegriffen werden.
```Csharp
class Car
{
	public string model = "Mustang";
}

class Program
{
	static void Main(string[] args)
	{
		Car myObj = new Car();
		// Output zeigt "Mustang" an
		Console.WriteLine(myObj.model);
	}
}
```

### Encapsulation 
*Encapsulation* bedeutet, dass man bestimmte Daten vor den Benutzern "versteckt". 
Um das zu tun muss:
- die Variable `private` sein
- es muss eine `get` und `set` Methode geben und ein Property 

Ein Property ist die Kombination aus einer Variable und Methoden:
```Csharp
class Person
{
	private string name; // field / variable
	
	public string Name // property
	{
		get { return name; }
		set { name = value; }
	}
}

class Program
{
	static void Main(string[] args)
	{
		Person myObj = new Person();
		myObj.Name = "John";
		Console.WriteLine(myObj.Name);
	}
}
```

You can also shorten these by just providing the property and methods `get;` and `set;`
```Csharp
class Person
{
	public string Name
	{get; set;}
}

class Program
{
	static void Main(string[] args)
	{
		Person myObj = new Person();
		myObj.Name = "john";
		Console.WriteLine(myObj.Name);
	}
}
```

```Csharp
public void SetFeldname(datentyp data)
{
	this.feldname = feldname;
}

public datentyp getFeldname()
{
	return feldname;
}
```
### Vererbung
Es ist möglich Klassen zu vererben, dabei wird unterschieden zwischen der *Kind-* und *Elternklasse*.
Zur Verarbeitung wird das Zeichen `:` benutzt
```Csharp
class Vehivle // Elternklasse
{
	public string brand = "Ford";
	public void honk()
	{
		Console.WriteLine("Tuuut, tuuut!);
	}
}

class Car : Vehicle //Kindklasse
{
	public string modelName = "Mustang";
}

class Program
{
	static void Main(string[] args)
	{
		Car myCar = new Car();
	}
}
```

# Working with Files
Dateien dienen der Speicherung von Daten auf einem Datenträger damit sie persistent sind, also nach dem Aus- und Einschalten des Rechners noch vorhanden sind.

Es gibt zwei Dateitypen:
- *Textdateien*:
  Daten sind mit beliebigem Texteditor oder Programm lesbar
- *Binärdateien*:
  Daten sind nur mit einem Programm lesbar.

Beide Dateitypen können als sequenzielle Datei oder als Random Access Datei realisiert werden
- *Sequenzielle Datei*: 
  Es kann nur am Anfang der Datei beginnend ein Datensatz nach dem anderen gelesen werden.
  Dies kann auch bei Festplatten verwendet werden.
- *Random Access*: 
  Es kann direkt auf einen beliebigen Datensatz lesend oder schreibend zugegriffen werden, ohne die davor lesen zu müssen.
  Voraussetzung ist, dass alle Datensätze exakt gleich lang und die Daten innerhalb als Spalten angeordnet sind.
## Lesen und Schreiben 

>[!note]
>Alle Versuche auf eine Datei zuzugreifen sollten in einem `try-catch-finally` Block stehen. 

 The `File` class from the `System.IO` namespace, allows us to work with files: 

```Csharp
using System.IO;

File.Method();
```

The Methods of the `File` class are:
- `AppendText()`: Appends text at the end of an existing file
- `Copy()`: Copies a file
- `Create()`:  Creates or overwrites a file
- `Delete()`: Deletes a file
- `Exists()`: Test whether the file exists
- `ReadAllText()`: Reads the contents of a file
- `Replace()`: Replaces the contents of a file with the contents of another file
- `WriteAllText()`: Creates a new file and writes the contents to it. If the file already exists it will be overwritten

```Csharp
using System.IO;

string writeText = "Hello World";
File.WriteAllText("filename.txt", writeText);

string readText = File.ReadAllText("filename.txt");
Console.WriteLine(readText);
```

Man kann optional noch eine gewünschte Codierung angeben.
- ASCII
- BigEndianUnicode
- Unicode
- UTF32
- UTF7
- UTF8

**Neue Datei anlegen und mit den Zahlen 1 bis 10 füllen**
```Csharp
File.WriteAllText("temp.txt", "");
// Mit Encoding
File.WriteAllText("temp.txt", "", Encoding.UTF8);

for (int i = 1; i < 11; i++)
{
	File.AppendAllText("temp.txt", String.Format($"{i}\n"));
}
```

**Textdatei mit einem Befehl komplett einlesen**
```Csharp
string text = File.ReadAllText("temp.txt");
// mit Encoding
string text = File.ReadAllTExt("temp.txt", Encoding.UTF8);
```

**Erzeugen einer CSV Datei**
```Csharp
File.WriteAllText("temp.txt", "");
for(int i = 1; i < 11; i++)
{
	File.AppendAllText("temp.txt", String.Format($"{i});{i * 1.5};{i + 2}\n"));
}
```

**Einlesen einer CSV Datei**
Es werden alle Zeilen eines Arrays eingelesen. Danach enthält jede Zelle des Arrays eine Zeile der Datei. Danach splitet man mit Split jede Zeile in Spalten auf. Dazu gibt man das in der Datei verwendeten Trennzeichen an. Danach wandelt man die spalten mit denen man rechnen will in einer Zahl mit dem entsprechenden Zahlenformat um.
```Csharp
string[] zeile = File.ReadAllLines("temp.txt");
for (int i = 0; i < zeile.Length; i++)
{
	string[] spalte = zeile[i].Split(';');
	// Verarbeitung der Spalten 
	int a = Int32.Parse(spalte[0]);
	double b = Double.Parse(spalte[1]);
	// ...
}
``` 

**Schreiben einer Datei**
Man kann Daten auch in einer String Variablen zuweise.
Jede Zeile muss dabei mit `\n` abgeschlossen werden, um einen Zeilenumbruch einzusetzen.
```Csharp
text = String.Empty;
for (int i = 1; i < 11; i++)
{
	text += String.Format($"{i}\n");
}
// Ausgabe
File.WriteAllText("tempt.txt", text);
```

Man kann die Daten auch einer generischen Liste hinzufügen. Jede Zeile entspricht dabei einer Zeile der Datei
```Csharp
List<String> liste = new List<string>();
for (int i = 1; i < 11; i++)
{
	liste.Add(i.ToString());
}
file.WriteAllLines("temp.txt", liste);
```

**Vorhandene Dateien ermitteln**
```Csharp
string[] dateien = Directory.GetFiles(@"c:\temp");
for (int i = 0; 1 < dateien.Length; i++)
{
	Console.WriteLine(dateien[i]);
}
```

oder
```Csharp
FileInfor[] fileInfo = directoryInfo.GetFiles();
foreach (FileInfo f in fileInfo())
{
	Console.WriteLine(f.Name);
}
```

**Dateien kopieren und verschieben**
```Csharp
// Kopieren
File.Copy(quelle, ziel);
File.Move(quelle, ziel);
```
# Verzeichnisse
Man benötigt wieder den namespace `System.IO`
```Csharp
using System.IO;
```

Wichtige Klassen sind:
- Directory
- DirectoryInfo
- File
- FileInfo

**Anlegen und Löschen eines Unterverzeichnisses**
```Csharp
(using System.IO;)

string verzeichnis = @"c:\temp\test";
// Anlegen
Directory.CreateDirectory(verzeichnis);
// Löschen
Directory.Delete(verzeichnis,true);
```

oder 
```Csharp
(using System.IO;)

DirectoryInfo directoryInfo = new DirectoryInfo(verzeichnis);
directoryInfo.Create();
directoryInfo.Delete(true);
```

**Unterverzeichnis verschieben**
```Csharp
(using System.IO;)

Directroy.Move(verzeichnis,@"c:\temp\ziel");
```

**Vorhandene Unterverzeichnisse ermitteln**
```Csharp
(using System.IO;)

string[] verzeichnisse = Directory.GetDirectories(verzeichnis);
for (int i = 0; i < verzeichnisse.Length; i++)
{
	Console.WriteLine(verzeichnisse[i]);
}
```

oder
```Csharp
(using System.IO;)

directoryInfo = new DirectoryInfo(@"c:\temp");
foreach (DirectoryInfo d in directoryInfo.GetDirectories())
{
	Console.WriteLine(d.Name);
}
```

**Alle Dateien und Unterverzeichnisse sowie deren Unterverzeichnisse mit Dateien ermitteln**
```Csharp
directoryIndo = new DirectoryInfo(@"c:\temp");
Console.WriteLine(directoryInfo.Name);
VerzeichnisseErmitteln(directoryInfo);

private void VerzeichnisseErmitteln(DirectoryInfo directoryInfo)
{
	foreach (DirectoryInfo d in directoryInfo.GetDirectories())
	{
		Console.WriteLine(d.Name);
		FileInfo[] fileInfo = d.GetFiles();
		foreach (FileInfo f in fileInfo)
		{
			Console.WriteLine("    " + f.Name);
		}
		VerzeichnisseErmitteln(d);
	}
}
```

**Dateiattribute ermitteln oder ändern**
```Csharp
FileInfo dateiInfo = new FileInfo(@"c:\temp\program.cs");
Console.WriteLine("Dateiattribute: ");
Console.WriteLine(dateiInfo.Exists);
Console.WriteLine(dateiInfo.Attributes);
Console.WriteLine(dateiInfo.CreationTime);
Console.WriteLine(dateiInfo.LastAccessTime);
Console.WriteLine(dateiInfo.LastWriteTime);

dateiINfo.LastWriteTime = new DateTine(2050, 12, 31, 1, 2, 3)
```

oder mit Klasse `File` und deren Methoden