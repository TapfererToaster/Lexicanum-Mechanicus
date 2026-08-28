Apache ist ein HTTP Webserver.


>[!note] LAMP Stack
>Der *LAMP Stack* ist ein Setup um Webapplikationen bereitzustellen
>- [[Linux]]
>- Apache
>- [[MySQL]]
>- PHP

Eigenschaften:
- *Apache Portable Runtime (APR)*:
  Die APR ist eine Abstraktionsbiliothek, die für systemnahe Funktionen wie Systemaufrufe oder Netzwerkverbindungen benutzt wird, und stellt diese für jedes Betriebssystem bereit.
- *Module als Dynamic Shared Objects (DSO)*:
  Ein Großteil der Funktionalität von Apache wird durch Module bereitgestellt die man in der Konfigurationsdatei ein- und abschalten kann, wodurch Erweiterungen durch dritte oder eigene Module erleichtert wird und nicht benötigte abgestellt werden können.

# Benutzen
Zur Steuerung des Servers wird die Datei `apachectl` benutzt:
- `apachectl start`: Apache starten
- `apachectl stop`: Apache beenden
- `apachectl graceful-stop`: Apache nach Bearbeitung der laufenden Clientanfragen beenden
- `apachectl restart`: Apache neustarten
- `apachectl graceful`: Apache nach Beendigung der der laufenden Clientanfragen neustarten

# Module
Module stellen einen Großteil der Funktionalität von Apache bereit, von diesen gibt es 70 die mit der Installation von Apache bereitgestellt werden.

- `mod_authz_host`: Zugriffsschutz basierend auf Client-Hostnamen und/oder IP-Adressen
- `mod_alias`: Erlaubt das Mapping von URLs zu Dateisystempfaden oder das Umleiten von Anfragen (z. B. für `/images` zu `/var/www/images`).
- `mod_auth_basic`: Modul zur Authentifizierung, nimmt die Anmeldedaten vom Client (unverschlüsselt) entgegen und prüft diese auf ihre Gültigkeit
- `mod_auth_digest`: Wie `mod_auth_digest` nur MD5-verschlüsselt.
- `mod_authn_dbd`: Sendet SQL-Abfragen an eine externe Datenbank, um Anmeldedaten zu überprüfen.
- `mod_authn_dbm`: Authentifizierungsprovider, welcher DBM Dateien verwendet.
- `mod_authn_file`: Authentifizierungsprovider, benutzt Text Dateien
- `mod_autoindex`: Erzeugt automatisch Verzeichnisindizes für Verzeichnisse ohne Indexdatei (Startseite), z. B. `index.html`.

- `mod_cache`: Implementiert Caching-Mechanismen, um häufig angeforderte Inhalte schneller bereitzustellen.

- `mod_cgi`: Führt CGI-Skripte aus, um dynamische Inhalte zu generieren (z. B. für ältere Skripte in Perl oder Bash).

- `mod_deflate`: Komprimiert die Ausgabedaten (z. B. HTML, CSS, JavaScript) vor dem Senden an den Client, um die Übertragungsgröße zu reduzieren.

- `mod_dir`: Ermöglicht die automatische Weiterleitung von Anfragen an Verzeichnisse zu einer Standarddatei (z. B. `index.html` oder `index.php`).

- `mod_expires`: Setzt Ablaufdaten für Inhalte, um Caching im Browser oder bei Proxys zu steuern.

- `mod_fcgid`: Ermöglicht das Ausführen von CGI- und FastCGI-Skripten (z. B. für PHP, Python oder Perl) mit besserer Performance und Sicherheit.

- `mod_headers`: Erlaubt das Hinzufügen, Ändern oder Entfernen von HTTP-Headern in Anfragen und Antworten.

- `mod_log_config`: Konfiguriert das Logging von Apache, einschließlich benutzerdefinierter Log-Formate und Dateipfade.

- `mod_mime`: Bestimmt den MIME-Typ von Dateien basierend auf ihrer Endung, um den Browsern mitzuteilen, wie die Daten interpretiert werden sollen.

`mod_php`: Integriert die PHP-Sprache in Apache, um dynamische Webseiten auszuführen. Wird oft mit `mpm_prefork` verwendet.

`mod_proxy`: Ermöglicht Apache, als Reverse-Proxy oder Forward-Proxy zu agieren, um Anfragen an andere Server weiterzuleiten.

`mod_rewrite`: Bietet eine leistungsstarke URL-Umschreibungs-Engine, um URLs dynamisch umzuleiten oder zu ändern (z. B. für SEO oder Weiterleitungen).

`mod_security`: Bietet eine Web Application Firewall (WAF), um Angriffe wie SQL-Injection oder Cross-Site-Scripting (XSS) abzuwehren.

`mod_ssl`: Ermöglicht die Nutzung von SSL/TLS-Verschlüsselung für sichere HTTPS-Verbindungen.

`mod_wsgi`: Integriert Python-Webanwendungen über das WSGI-Protokoll (Web Server Gateway Interface) in Apache.

`mod_authz_core`: Steuert den Zugriff auf Ressourcen basierend auf Benutzerrechten und Gruppen (z. B. für passwortgeschützte Bereiche).

`mpm_event`: Optimiert für hohe Parallelität, besonders für Keep-Alive-Verbindungen. Nutzt Threads für die Anfragebearbeitung und ist ideal für moderne Webserver.

`mpm_prefork`: Verwaltet Prozesse für Apache, indem es für jede Anfrage einen separaten Prozess erstellt. Ideal für Umgebungen, die Stabilität über Performance stellen (z. B. mit PHP und mod_php).

`mpm_worker`: Nutzt einen hybriden Multi-Prozess- und Multi-Thread-Ansatz, um Anfragen effizienter zu bearbeiten. Gut für Hochlastumgebungen mit statischen Inhalten oder PHP über FastCGI.

# Konfiguration