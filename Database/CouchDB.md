CouchDB ist eine Open-Source [[Databases#Dokumentorientierte Datenbanken|dokumentenbasierte Datenbank]].

Diese ist dabei ein Webserver der über den TCP-Port 5984 kommuniziert. Anfragen werden dabei über eine [[(API) Application Programming Interface|RESTful API]] angenommen und Antworten im JSON-Format gesendet.
Zusätzlich gibt es Bibliotheken für gängige Programmiersprachen.

Als Administrationsoberfläche wird [Fauxton](https://docs.couchdb.org/en/stable/fauxton/index.html) bereitgestellt und kann in einem Webbrowser über `http://ip-address:5984/_utils/` aufgerufen werden.

Beim erstellen eines neuen Dokuments wird ein MD5-Zufallswert generiert, danach kann man beliebige Felder definieren.
**Beispiel**:
```JSON
{ "_id" "8e31cf918831d547d77845b157003823",
  "lastname" "Müller",
  "firstname" "Maggus", 
  "email" "maggus.mueller@example.de" }
```

Um eine Abfrage zu stellen:
```SQL
{ "selector": 
  { "lastname" "Müller" } 
}
```

