# Muster
Ein regulärer Ausdruck beschreibt standardmäßig keinen kompletten String, sondern einen Teil-String der im gesuchten String enthalten ist. 
Die Teil-Strings werden als Muster angegeben
- `abc`: gibt die gesuchten Zeichen an
  `ee`-> Tee, See, Teer
- `[ab]`: steht für ein Zeichen aus der Liste
  `[HM]aus`-> Haus, Maus
- `[a-z]`: steht für den angegebenen Zeichenbereich; auch Zahlen können angegeben werden
- `[^abc]`: steht für jedes beliebige Zeichen ausgeschlossen den Zeichen aus der Liste
  `[^M]aus` -> Haus, raus 
- `.`: steht für genau ein beliebiges Zeichen
  `.aus`-> Haus, Maus, raus

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
