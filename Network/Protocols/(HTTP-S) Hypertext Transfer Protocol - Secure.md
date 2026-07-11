- https://developer.mozilla.org/en-US/docs/Web/HTTP

When using a browser HTTP and HTTPS are mainly used, which rely on TCP and define your web browser communicates with the web servers.

HTTP and HTTPS usually use TCP ports 80 and 443, less commonly 8080 and 8443

# Kommunikation
1. Der Browser zerlegt die URL in Schema, Hostname, Portnummer und Pfad zur Resource
2. Per [[(DNS) Domain Name System|DNS]] wird die IP-Adresse des Ziels ermittelt und eine TCP Verbindung aufgebaut
3. Der Browser sendet eine HTTP-Anfrage bestehend aus HTTP-Methode, Pfad und Protokollversion.
4. Der Server empfängt die Anfrage und sendet eine Antwort und bei Erfolg die gewünschte Resource. Im Header der Antwort wird mit einer Codenummer der Status der Anfrage beschrieben.

# Header
https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers
 
 **Allgemeine Header**
- `Cache-Control`: Steuert das Caching-Verhalten 
- `Connection`: Steuert die Netzwerkverbindung 
- `Date`: Zeitstempel, wann die Anfrage/Antwort generiert wurde

**Anfrage-Header (Request)**
- `Accept`: Gibt an, welche Inhaltsformate der Client akzeptiert 
- `Accept-Encoding`: Unterstützte Komprimierungsmethoden 
- `Accept-Language`: Bevorzugte Sprache des Clients 
- `Authorization`: Authentifizierungsdaten 
- `Host`: Domain des Servers 
- `User-Agent`: Informationen über den Client 
- `Cookie` : Sendet gespeicherte Cookies an den Server
- `Referer`: URL der vorherigen Seite, von der die Anfrage stammt

**Antwort-Header (Response)**
- `Server`: Informationen über den Server 
- `Set-Cookie`: Setzt Cookies im Client 
- `Location`: URL für Umleitungen 
- `WWW-Authenticate`: Fordert Authentifizierung an 

 **Entity-Header (Inhaltsbezogen)**
- `Content-Type`: Typ des Inhalts 
- `Content-Length`: Größe des Inhalts in Bytes
- `Content-Encoding`: Angewandte Komprimierung 
- `Content-Language`: Sprache des Inhalts 
- `Last-Modified`: Zeitstempel der letzten Änderung der Ressource

**Sicherheitsheader**
- `Strict-Transport-Security (HSTS)`: Erzwingt HTTPS 
- `X-Content-Type-Options`: Verhindert MIME-Sniffing 
- `X-Frame-Options`: Steuert das Einbetten in Frames 
- `X-XSS-Protection`: Aktiviert XSS-Schutz im Browser 
- `Content-Security-Policy (CSP)`: Definiert erlaubte Ressourcenquellen
- `Cross-Origin-Opener-Policy (COOP)`: Steuert Cross-Origin-Isolation 
- `Cross-Origin-Resource-Policy (CORP)`: Steuert, wer Ressourcen laden darf 

**Performance & Tracking**
- `ETag`: Eindeutiger Identifier für eine Ressourcenversion (für Caching).
- `If-None-Match`: Vergleicht ETags für bedingte Anfragen.
- `If-Modified-Since`: Prüft, ob sich die Ressource seit einem Datum geändert hat.

**API-spezifisch**
- `Origin`: Ursprung einer CORS-Anfrage 
- `Access-Control-Allow-Origin`: Erlaubte Ursprünge für CORS 
- `Access-Control-Allow-Methods`: Erlaubte HTTP-Methoden
- `Access-Control-Allow-Headers`: Erlaubte Header in CORS-Anfragen
# Request and Response
## Requests /Methods
The commands and methods used by the web browser to the web server are:
- `GET` retrieves data from a server (HTML file or an image)
- `POST` submits new data to the server (submitting a form or uploading a file)
- `PUT` used to create a new resource on the server and to update and overwrite existing information
- `DELETE` used to delete a specific file or resource on the server
- `PATCH` used to update a resource object
- `LINK` Verknüpfung erzeugen
- `UNLINK` Verknüpfung löschen
- `TRACE` Proxys anzeigen
- `CONNECT` Proxy-Zugriff auf gesicherte Server
- `OPTIONS` Liste verfügbarer Optionen anfordern

>[!note]
>[[(Telnet) Teletype Network|Telnet]] can be used to connect to web servers and communicate with them.

Diese Methoden werden dann zusammen mit mehreren Headerwerten als *Query-String* versendet.
**Beispiel einer GET-Request**
```HTTP
GET / HTTP/1.1 
Host: example.com 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36 
Accept: */*
Accept-Encoding: gzip, deflate, br 
Accept-Language: de,en-US;q=0.9,en;q=0.8 
Connection: keep-alive 
```

>[!note]
>`GET` Requests können auch Formulardaten versenden, diese werden im Format `feld1=wert1&feld2=wert2` dann mit einem Fragezeichen an die URL angehängt
## Responses

| **Response Code** | **Description** |
| ----------------- | --------------- |
| 1XX               | Informational   |
| 2XX               | Successful      |
| 3XX               | Redirect        |
| 4XX               | Client error    |
| 5XX               | Server error    |


**Beispiel einer Response**
```HTTP
HTTP/1.1 200 OK 
Content-Type: text/html; charset=UTF-8 
Content-Length: 1256 
Connection: keep-alive 
Date: Sat, 11 Jul 2026 12:00:00 GMT 
Server: nginx 
```

### Statuscodes

>[!info]
>Weitere [Statuscodes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) 

**1xx - Informational**
- `100 Continue`: Anfrage erhalten, der Server erwartet eine Fortsetzung.
- `101 Switching Protocol`: Der Server möchte auf die im Header angegebene HTTP-Version wechseln.

**2xx - Successful**
- `200 OK`: Anfrage war erfolgreich und die angeforderte Ressource wird geliefert.
- `201 Created`: Die `POST` Anfrage war erfolgreich und die Datei wurde auf dem Server gespeichert.
- `202 Accepted`: Die Anfrage wurde erfolgreich verarbeitet.
- `203 Non-Authoritative`: Die Gültigkeit der gesendeten Informationen konnten nicht verifiziert werden, da sie von einem Proxy stammen. 
- `204 No Content`: Die Anfrage ist gültig, die Antwort enthält keinen Body.
- `205 Reset Content`: Der Client soll das Formular zurücksetzen
- `206 Partial Content`: Die Anfrage enthält nur einen Teil der Ressource, siehe `Content-Range` im HTTP Header

**3xx - Redirect**
- `300 Multiple Choices`: Es sind mehrere Alternativen der Ressource verfügbar, eine Liste mit entsprechenden Links ist im Body verfügbar.
- `301 Moved Permanently`: Die Ressource wurde dauerhaft an einen anderen Ort verschoben, siehe `Location` im HTTP Header.
- `302 Found`: Die Ressource wurde vorübergehend verschoben.
- `303 See Other`: Die Ressource ist unter einer anderen URL zu finden

**4xx - Client Error**
- `400 Bad Request`: Ungültige Anfrage 
- `401 Unauthorized`:  Authentifizierung erforderlich
- `403 Forbidden`:  Zugriff verboten
- `404 Not Found`:  Ressource nicht gefunden
- `405 Method Not Allowed`:  HTTP-Methode nicht erlaubt
- `408 Request Timeout`: Zulässige Wartezeit abgelaufen
- `429 Too Many Requests`:  Zu viele Anfragen (Rate Limiting)

**5xx Server Error**
- `500 Internal Server Error`: Server-Fehler
- `502 Bad Gateway`: Ungültige Antwort vom Server oder Proxy
- `503 Service Unavailable`: Server vorübergehend nicht verfügbar
- `504 Gateway Timeout`: Timeout beim Server oder Proxy
# HTTPS
HTTPS is the secure version of HTTP, meaning that the data is encrypted when transferred.
This is made possible by using (TLS) Transport Layer Security.
A HTTPS request consists of the following steps:
1. Establish a TCP three-way handshake
2. Establish a TLS session
3. Communicate using the HTTP protocol