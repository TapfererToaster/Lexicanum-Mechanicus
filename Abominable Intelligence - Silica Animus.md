# Machine Learning
Machine Learning Verfahren lernen selbständig aus strukturierten Datenmengen, indem sie die ein eigenes Modell dieser Daten optimieren, um die beste Lösung zu finden.
Es wird zwischen drei Arten unterschieden:

**Supervised Learning** (Überwachtes Lernen)
Die Algorithmen erhalten als erstes Beispieldaten, bei denen die gewünschten Schlussfolgerungen schon bekannt sind. Dadurch wird ihnen Schritt für Schritt die Interpretation solcher Daten beigebracht, bis die gleichartig organisierte Daten mit unbekannter Schlussfolgerung interpretieren können.
Werden die Algorithmen nicht genug trainiert kommt es zu *Underfitting*, hierbei werden selbst die Trainingsdaten nicht gut interpretieren können. 
Wird zu viel trainiert, liefert der Algorithmus richtige Ergebnisse für Testdaten, jedoch falsche Ergebnisse für Testdaten.

**Unsupervised Learning** (Unüberwachtes Lernen)
Der Algorithmus erhält keine Beispieldaten, sondern muss selbst die Daten interpretieren und in Kategorien einteilen.

**Reinforced Learning** (Verstärktes Lernen)
Der Algorithmus wird für richtige Interpretation von Daten belohnt und für falsche bestraft, indem Punkte in einem Bewertungsschema verstärkt bzw. abgeschwächt werden.
## Algorithmen
Machine Learning wird typischerweise eingesetzt für die Lösung von 
- *Klassifikationsprobleme*:
  aufgrund von statistischen Eigenschaften von Daten wird versucht diese in Kategorien einzuordnen
- *Regressionsprobleme*:
  anhand von einer bekannten Liste wird versucht einen Wert für ein unbekanntes Element zu schätzen

Die Algorithmen die zur Lösung solcher Probleme eingesetzt werden sind in verschiedene Klassen unterteilt:

*Linear Regression*
  Es wird eine lineare Funktion gesucht, die den Verlauf von bekannten Datenpunkten in einer Datenmenge so genau beschreibt, dass sich für unbekannte Punkte ein Wert vorhersagen lässt.
  Werden für Regressionsprobleme benutzt

*Logistic Regression*
  Es werden lineare Funktionen gesucht, die Trennlinien zwischen Datenkategorien bilden.
  Werden für Kategorisierung benutzt

*Decision Trees*
  Decision Trees werden erstellt, indem Trainingsdaten aus verschiedenen Kategorien nach abgrenzenden Merkmalen untersucht werden, um als Abfolge von Fallentscheidungen auf Daten angewendet werden können.
  Werden für Kategorisierung benutzt

*Naive Bayes-Klassifikatoren*
  Die Klassifikatoren stellen vereinfachte Annahmen über Daten, weswegen sie "naiv" genannt werden, die dennoch ein brauchbares Ergebnis liefern.
  >[!note] 
  >Die Klassifikatoren basieren auf dem Satz von Bayes aus der Statistik, welcher die Berechnung abhängiger Wahrscheinlichkeiten ermöglicht.

### Lineare Regression
Bei der *linearen Regression* wird eine Gerade gesucht, die möglichst genau den Verlauf mehrerer Datenpunkte beschreibt.

### Logistische Regression
Die *logistischen Regression* ist ein Klassifikationsverfahren, bei der Daten in zwei verschiedene Klassen eingeteilt werden die den Werten 1 und 0 zugeordnet bekommen.
Bei mehreren Kategorien und Klassifizierungen, wird das *One vs. All* Verfahren benutzt, bei dem die von ihnen vertretene Kategorie den Wert 1 bekommt und alle anderen den Wert 0.

Als Funktion kommt dabei eine Sigmoid-Funktion zum Einsatz.

Zur Minimierung der Kostenfunktion wird ein *gradient descent* (Gradientenabstieg) verwendet, indem man in kleinen Schritten (*Learning Rate*) sich an die Funktion anzunähern. Die Learning Rate erhält dabei einen Wert zwischen 0 und 1, dieser wird mit einem Modifikationswert multipliziert wird um seinen Einfluss pro Durchgang zu mildern.

### K-Means Clustering

> [!NOTE]
> Bei *Clustering* werden Daten in eine bestimmte Anzahl *k* in Cluster (Gruppen) unterteilt, wobei unüberwachtes Lernen zum Einsatz kommt und von Anfang an mit echten Daten gearbeitet wird.

*K-Means* ist einer der bekanntesten Clustering-Algorithmen, der mit Mittelwerten arbeitet.
Der Ablauf ist:
1. Für jedes Cluster wird ein *Zentroid* erzeugt, ein Array mit genauso vielen Werten, wie es Datensätze gibt
2. Alle Werte der Datenmenge werden dem Cluster zugeteilt, dessen Zentroid am nächsten liegt.
   Für die Berechnung wird der [euklidische Abstand](https://de.wikipedia.org/wiki/Euklidischer_Abstand) benutzt.
3. Der Mittelwert der Cluster wird berechnet und als deren neues Zentroid festgelegt.
4. Haben sich die Zentroide nicht verschoben ist der Algorithmus beendet; sollte eine festgelegte Anzahl an Durchläufen nicht erreicht sein geht es mit Schritt 2 weiter
# Datenanalyse
## Aufbereitung
Bevor Daten analysiert werden können müssen sie nummerisch interpretiert werden.
### Textdateien 
#### Bag of Words 
Texte die nach den enthaltenen Wörtern ausgewertet werden sollen, werden oft als "*Bag of Words*" kodiert, indem die Strings in einzelne Wörter zerlegt werden und für jeden String ein Array erstellt wird indem die in ihm enthaltenen Wörter gespeichert werden. 

Müssen viele oder lange Strings aufgearbeitet werden, können die Arrays zu lang werden, weswegen es sinnvoll ist die Strings zu reduzieren. Dafür werden *Stoppwörter*, die nicht für die Klassifikation relevant sind, wie Artikel oder Konjunktionen die in jedem Text vorkommen, herausgefiltert. Jedoch können auch einzeln vorkommende Wörter weggelassen werden, da sie eventuell als statistische Ausreißer Probleme bereiten könnten. 
#### N-Gramme
Manchmal sind Wortfolgen statt einzelne Wörter aussagekräftiger, solche Wortfolgen nennt man *N-Gramme*, wobei `N` für die Anzahl der gemeinsam betrachteten Wörter, z.B. Bigramme (zwei Wörter), Trigramme (drei Wörter) etc..
### Bilddateien
Für Bilddateien werden, mit oder ohne Kompression, die Farbwerte für jedes einzelne Pixel gespeichert. Jedoch müssen diese Werte reduziert werden, da es oft zu viele Pixel- und Farbwerte gibt, z.B. bei einem 100x100 Pixel großen Bild insgesamt 10.000 Pixel und bei 256 Stufen für Rot, Grün und Blau gibt es insgesamt 16,7 Millionen Werte.
### Nummerische Daten visualisieren
Es ist sehr hilfreich nummerische Daten in geeigneten Darstellungen zu visualisieren, etwa in Form eines Diagramms.

# Neuronale Netze
*Artifical Neural Networks (ANN)*, dt. Künstliche neuronale Netzwerke bestehen aus mehreren Schichten von künstlichen Neuronen, die stark vereinfachte Modelle natürlicher Neuronen sind. 

Die Neuronen sind dabei in mindestens drei Schichten angeordnet:
**Input Layer**:
Nimmt die Eingabewerte auf, hat so viele künstliche Neuronen wie die eingegebene Datenmenge Features hat.

**Hidden Layer**:
Eine oder mehrere versteckte Schichten verarbeiten die eingegebenen Daten, je nach Problem können diese auch die Daten filtern oder vereinfachen

**Output Layer**:
gibt das Ergebnis aus
>[!note]
>Bei Klassifikationsproblemen gibt es ein Neuron pro Kategorie, das mit dem höchsten Ausgabewert ist die Kategorie des untersuchten Datensatzes.

*Backpropagation* wird als Verfahren benutzt um die Gewichte der künstlichen Neuronen anzupassen indem die Abweichung von Soll- und Ist-Werten rückwärts durch die versteckten Schichten verteilt werden. Dazu wird die Ableitung der Aktivierungsform der Aktivierungsfunktion auf den Fehler angewendet und anschließend werden die Gewicht damit multipliziert.
## Künstliche Neuronen
*Künstliche Neuronen* haben mehrere Eingänge über die Werte eingegeben werden können, zusätzlich besitzt das künstliche Neuron genauso viele *Gewichte* in Form von Fließkommazahlen, welche am Anfang Zufallswerte bekommen. Diese Gewichte sind die trainierbaren Parameter, welche mit den Eingangswerten zu einem Skalarprodukt verrechnet werden, dieses wird mit einer *Aktivierungsformel* modifiziert und wenn das Ergebnis relevant ist, an die Neuronen der nächsten Schicht weitergegeben.

>[!note]
>Eine typische Aktivierungsfunktion wäre die Sigmoid-Funktion.
>Weitere Funktionen sind:
>- *tanh-Funktion* (hypyerbolischer Tangens):
>   Wertebereich zwischen -1 und 1, Mittelwert bei 0; günstigere Verarbeitung und selteneres Auftreten von *Vanishing-Gradient-Problem* 
>- *RELU-Funktion* (Rectified Linear Unit):
>  negative Werte werden auf 0 gesetzt, positive bleiben erhalten; schneller als Sigmoid und tanh Funktion, Vanishing-Gradient-Problem tritt nicht auf
>- *Leaky ReLU*:
>  negative Werte werden nicht auf 0 gesetzt, sondern mit einem kleinen positiven Wert multipliziert; verhindert, dass Neuronen durch den Wert 0 ausgeschaltet werden.


## Feedforward Networks
Das *Feedforward Netzwerk* ist die einfachste From eines neuronalen Netzwerkes, dabei geht der Datenfluss von der Eingabeschicht über die aufeinanderfolgenden versteckten Schichten zur Ausgabeschicht.

Das Lernen erfolgt durch eine *Backpropagation*, die Trainingsdaten werden von den Sollwerten abgezogen und rückwärts durch das Netzwerk geschickt, wodurch die Gewichte bei jedem Lernschritt besser an die Trainingsdaten angepasst werden. Hierbei wird auch eine Lernrate benutzt, um die Größe der Schritte zu bestimmen.

## Rekurrente neuronale Networks
In *rekurrenten neuronalen Netzwerken* fließen Daten nicht nur in eine Richtung, da verschiedene Formen der Rückkopplung, bei der Neuronen Daten an eine vorherige Schicht leiten können.
Diese Netzwerke können Probleme lösen die aus mehreren zusammenhängenden Datensätzen und Datensequenzen bestehen lösen, und werden zur Erkennung von Bildern, handgeschriebenen Texten und gesprochener Sprache angewendet.

Eine bekannte Implementierung ist das *Long Short-Term Memory (LSTM)*, das Informationen länger speichern kann. Hierfür besitzen die künstlichen Neuronen neben dem *Input Gate* (Eingang) und *Output Gate* (Ausgang), auch *Forget Gate*, das bestimmt wie lange ein Wert gespeichert ist.
Für die Gates werden verschiedene Aktivierungsfunktionen und Vektor- und Matrixoperationen verwendet.

>[!note]
>LSTM können auch neue Daten, wie in Form von Texte oder Bildern, generieren.

## Convolutional Neural Networks
Bei *Concolutional Neural Networks* werden, neben Gewichtungen, auch *Faltungsfunktionen* verwendet, die beschreiben wie Funktionen die From von anderen Funktionen modifizieren. Dies verbessert die Performance der Datenverarbeitung und bei richtiger Implementierung verringert es nicht die Genauigkeit des Netzwerkes.
Anwendungen sind die Bilderkennungen, das dieses Netzwerk Kanten, Kontraste und Muster in Bildern gut erkennen kann.

## Deep-Learning Networks
*Deep-Learning Netzwerke* sind neuronale Netzwerke die aus vielen versteckten Schichten, die oft unterschiedliche Aufgaben erledigen, bestehen und mit möglichst vielen Trainingsdaten und Durchläufen trainiert werden.

## Generative Adversarial Networks
Hier treten zwei Deep-Learning Networks gegeneinander an, indem eines eine Aufgabe erfüllt und das andere die Lösung bewertet. Dadurch werden die Lösungen des ersten Netzwerks verbessert

# Large Language Models (LLMs)
Bei *Large Language Models* werden Wortfolgen und Texte in einer vieldimensionalen Matrix aufbereitet und damit wird aufgrund des bisherigen Textes das nächste Wort mit einem Wahrscheinlichkeitswerts vorhergesagt. Der vorhandene Text ist dabei der eingegebene Prompt und auch der bereits erzeugt Teiltext.

Large-Language Models basieren auf dem *Transformer-Modell* , welches aus zwei Hauptkomponenten besteht:
- *Encoder*
  nimmt eine Satz als Eingabesequenz auf, erteilt jedem Token der Eingabe einen Positionswert und erstellt eine abstrakte Repräsentation, welche an den Decoder weitergegeben wird.
- *Decoder*
  Generiert eine Ausgabe basierend auf der Repräsentation des Encoders, indem er die Wahrscheinlichkeit des nächsten Wortes aufgrund des vorherigen bestimmt.

Benutzt wird das *Multi-Head-Attention-Mechanism*, bei dem durch mehrere parallele Berechnungsstränge (*Heads*) die Aufmerksamkeit (*Attention*) auf verschiedene Aspekte der Eingabe konzentriert werden, so etwa semantische oder syntaktische Beziehungen. 