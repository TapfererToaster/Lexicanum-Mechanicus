# Algorithmen
## Planung und Implementierung
Bevor ein Algorithmus in einer Programmiersprache als Computerprogramm implementiert wird, sollte dessen Ablauf in leichter und verständlicher Form aufgeschrieben werden.
Hierfür gibt es mehrere Möglichkeiten man:
- eine nummerierte Liste mit den einzelnen Schritten 
- ein Flussdiagramm
- ein Struktogramm

Nach dem der Ablauf und die einzelnen Schritte des Algorithmus erarbeitet wurden kann man den Algorithmus in Pseodocode schreiben, um die Erstellung des eigentlichen Codes zu erleichtern. 

Abschließend wird der Algorithmus in einer Programmiersprache als Programm implementiert.

### Beispiel: Algorithmus von Euklid
**Planung**
Nummerierte Liste:
1. Wenn die zweite Zahl 0 ist, wird die erste zurückgegeben
2. Die zweite Zahle wird durch den Rest ersetzt, der bei der Division der ersten durch die zweite entsteht.
3. Die erste Zahl wird durch den vorherigen Wert der zweiten ersetzt
4. Es geht weiter bei Punkt 1

Flussdiagramm:
![[Flussdiagramm Euklid.png|469]]
**Implementierung**
```python
def EuklidAlgo(zahl1, zahl2):
	while zahl2 != 0:
		rest = zahl1 % zahl2
		zahl1 = zahl2
		zahl2 = rest
	return zahl1
	
# Alternative
def EuklidAlgo(zahl1, zahl2):
	while zahl2 != 0:
		zahl1, zahl2 = zahl2, zahl1 % zahl2
	return zahl1
```

# Sortieralgorithmen

>[!note]
>Programmiersprachen haben schon vorhandene Sortieralgorithmen, es ist nicht erforderlich oder effizient eigene Implementierungen der Sortieralgorithmen in der Praxis zu schreiben.

## Bubblesort
Bei diesem Algorithmus werden die nebeneinanderliegenden Elemente miteinander verglichen, sind diese in der falschen Reihenfolge werden sie vertauscht. Dieser Vorgang wird dann so oft wiederholt, bis alle Elemente in der richten Reihenfolge sind.
```python
def bubblesort(list):
	while True:
		is_sorted = True
		for i in range (0, len(list)-1):
			if list[i] > list[i + 1]:
				list[i], list[i+1] = list[i+1], list[i]
				is_sorted = False
		if is_sorted:
			break
```

## Quicksort
Bei diesem Algorithmus wird das zu sortierende Array in zwei Teile geteilt, welche an rekursive Aufrufe der Funktion übergeben werden. Aus den Teilgruppen wir ein zufälliges Vergleichselement gewählt, *Pivot* genannt. Elemente die größer sind als das Pivot, werden nach rechts von diesem einsortiert, kleinere Elemente nach links. Dies wird so lange wiederholt bis nur noch zwei Elemente übrig sind, die in die richtige Reihenfolge gebracht werden.
```python
def partition(array, low, high):  
  pivot = array[high]  
  i = low - 1  
  
  for j in range(low, high):  
     if array[j] <= pivot:  
       i += 1  
       array[i], array[j] = array[j], array[i]  
  
  array[i+1], array[high] = array[high], array[i+1]  
  return i+1  
  
def quicksort(array, low=0, high=None):  
  if high is None:  
    high = len(array) - 1  
  
  if low < high:  
    pivot_index = partition(array, low, high)  
    quicksort(array, low, pivot_index-1)  
    quicksort(array, pivot_index+1, high)
```

# Komplexität
# Daten suche
Häufig wird in Programmen nach Elementen in einem *Search Space*, der aus verschiedenen Datenstrukturen bestehen kann.
## Listen
### Lineare suche
Bei der linearen Suche nach Elementen werden die vorhandenen Elemente nacheinander mit dem gesuchten Wert verglichen. Wenn der Suchwert gefunden wird, wird dessen Index zurückgegeben.
**Implementierung**
```python
def linearSearch(list, value):
	for i in range(0,len(list)):
		if list[i] == value:
			return i
			
	return -1	
```

### Binäre Suche
Die binäre Suche erfordert ein bereits sortiertes Array, welches durch eine rekursive Methode unterteilt wird um das gesuchte Element schneller zu finden.
**Implementierung**
```python
def binarySearch(list, targetVal):  
  left = 0  
  right = len(list) - 1  
  
  while left <= right:  
    mid = (left + right) // 2  
  
    if list[mid] == targetVal:  
      return mid  
  
    if list[mid] < targetVal:  
      left = mid + 1  
    else:  
      right = mid - 1  
  
  return -1
```

## Nicht sequenzielle Datenstrukturen
Manche Datenstrukturen haben keine vorgegebene Ordnung die sequenziell durchsucht werden kann, bei diesen ist es wichtig, dass die bereits durchsuchten Elemente gemerkt werden, da es ansonsten dazu kommen kann, dass der Algorithmus nicht endet.
Die Menge die noch zu durchsuchen ist wird *Frontier* genannt. Damit als Ergebnis ein Weg geliefert wird und nicht nur das gesuchte Element, besteht die Frontier nicht nur aus den zu dursuchenden Zuständen, sondern aus Instanzen einer Datenstruktur die den bisher eingeschlagenen Weg kapselt, indem sie auf ein Parent-Element verweist.

> [!NOTE]
> Hier wird als Beispiel die Pfadsuche durch eine Labyrinth angenommen.
>Die Vorgehensweise beim Labyrinth ist die gleiche wie bei Graphen

>[!note]
>Visualisierung der Algorithmen mit Labyrinthen: https://algo-vz.netlify.app/#
>
### Depth-First Search
>[!note]
>[Visualisierung](https://algorithm-visualizer.org/brute-force/depth-first-search) des Algorithmus

Dieser Suchalgorithmus geht jeden Weg solange bis er an nicht weiter kann oder den Ausgang gefunden hat. Bei einer Weggabelung, wo es mehrere Nachfolgezustände gibt, werden die Frontier (Nachfolgezustände) auf einen Stack gelegt und nach dem Last in, first out Prinzip  bearbeitet. Dadurch werden viele Wege nicht beschritten und es wird der erste zum Ausgang führende Weg ist das Ergebnis und nicht notwendigerweise der schnellste.
### Breadth-First Search
>[!note]
>[Visualisierung](https://algorithm-visualizer.org/brute-force/breadth-first-search) des Algorithmus

Dieser Algorithmus geht nicht jeden Weg bis zum Ende oder zu einer Sackgasse, sondern probiert jeden möglichen Zustand auf jedem möglichen Weg einzeln durch. Dadurch dauert dieser länger als der Depth-First Search Algorithmus und verbraucht auch mehr Ressourcen, liefert jedoch den kürzesten Weg zurück.
Hierbei wird die Frontier auf als Queue (Warteschlange) gespeichert und nach dem First in, first out Prinzip bearbeitet.

### A* Search Algorithm
Der *A-Star* Algorithmus ist *informierter* Suchalgorithmus, es werden also bekannt Informationen über das Ziel und die Entfernung zu diesem verwendet um das Ergebnis zu optimieren. 
Hierzu werden die Kosten des Weges zum aktuellen Element gespeichert und die Kosten des restlichen Weges zum Ziel geschätzt. 
Die Frontier wird als Priority Queue gespeichert, bei der das günstigste Element als erstes bearbeitet wird.

# Constraint Satisfaction Problems
*CPS* (Bedingungserfüllungsprobleme) sind Probleme bei denen mehrere Anforderungen erfüllt werden müssen, ohne dass ein Konflikt zwischen ihnen entsteht. 
Algorithmen die zur Lösung dieser eingesetzt werden haben drei Komponenten:
- *Variables*:
  Die einzelnen Elemente, für die konfliktfreie Werte gesucht werden
- *Domains*:
  Listen der möglichen Werte für die Variablen
- *Constraints*:
  Die Anforderungen die eine Wertezuordnung (*Assignment*) erfüllen muss, um als Lösung zu gelten

Beim Ausführen werden Kombinationen als Lösungsmenge akzeptiert, bis ein Widerspruch entsteht. Sobald das geschieht wird zu einer vorherigen Variable zurückgekehrt, deswegen heißt es *Backtracking* Suchverfahren.
  
# Datenstrukturen
## Graphen
![[Graph.png|325]]
Ein Graph besteht aus einer Menge von Elementen (*Vertices*, Singular *Vertex*) zwischen denen es beliebige richtungslose Verbindungen (*Edges*) geben kann. Daher wird ein Graph als Tupel (V,E) definiert mit einer Elementmenge *V* und einer Verbindungsmenge *E*.

Unterformen der Graphen sind
- *Diagraph* (gerichteter Graph): die Edges haben eine Richtung, die in Zeichnungen durch Pfeile dargestellt werden; Diagraphen die keine Multigraphen sind bestehen nur aus "Einbahnstraßen"
- *Multigraph*: zwischen identischen Vertices kann es beliebig viele Edges geben
- *gewichteter Graph*: die Anzahl von mehrfachen Verbindungen wird als *Kantengewicht* benutzt um Wege zu bewerten
## Bäume
![[Bäume.png|312]]
Bäume sind eine Sonderform von Graphen und werden häufig für verzweigte oder verschachtelte Informationen eingesetzt. 
Die einzelnen Elemente in einem Baum werden *Nodes* (Knoten) genannt, wobei eine Node nur einen Parent, jedoch mehrere Children haben kann.

Die wichtigste Art von Bäumen sind *Binärbäume*, bei diesen kann ein Knoten maximal zwei Children haben, und werden für die Implementierung von Such- und Sortieralgorithmen verwendet. 
>[!note]
>Die innere Datenstruktur einer Priority Queue ist ein Binärbaum.











