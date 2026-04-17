```XML
<?xml version="1.0" encoding="UTF-8" ?> 
<document>
	<paragraph> Dies ist ein XML-Dokument.</paragraph>
	<paragraph> 
		Zeile <emphasis>vor</emphasis> Umbruch <break />
		Zeile <emphasis>nach</emphasis> Umbruch
	</paragraph>
	<!-- Es folgt eine Liste -->
	<list type = "numbered">
		<item>XML ist strukturiert.</item>
		<item><![CFATA[Elemente werden so geschrieben: <element>...</element>]]>
		<item>Kommentare sehen so aus: &lt;!-- Kommentar --&gt;</item>
	</list>
<document>
```
# Regeln
- XML-Dokumente beginnen mit einer `<?xml ?>` Steueranweisung,  der XML Version `version="1.0"` und der dem Zeichensatz `encoding="UTF-8"` 
- Elemente werden mit `<elementname>` geöffnet und mit `</elementname>` geschloßen
  Elemente in spitzen Klammern heißen *tags*
- Alle Elemente sind von einem *Wurzelelement* umschloßen; z.B. `<document> ... </document>`
- Elemente müssen korrekt verschachtelt werden, das letzte geöffnete Element muss als erstes wieder geschloßen werden
```XML
<!-- Falsch -->
<element1>
	<elment2>
</element1>
	</element2>
	
<!-- Richtig -->
<element1>
	<element2>
	</element2>
</element1>	
```
- Elementnamen dürfen Buchstaben, Ziffern, Unter- und Bindestriche enthalten, müssen aber mit einem Buchstaben beginnen
- Elemente können auch Attribute enthalten `attribut=wert`, diese werden innerhalb der spitzen Klammern des öffnenden Tags geschrieben und werden im schließenden Tag nicht wiederholt

> [!NOTE]
> - it must begin with the XML declaration
> - it must have one unique root element
> - start-tags must have matching end-tags
> - elements are case sensitive
> - all elements must be closed
> - all elements must be properly nested
> - all attribute values must be quoted
> - entities must be used for special characters
