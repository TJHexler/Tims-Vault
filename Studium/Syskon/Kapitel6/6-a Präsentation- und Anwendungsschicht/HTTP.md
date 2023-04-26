---
tags: Uni Syskon
---
# Hyper Text Transfer Protocol (HTTP)
Protokoll (HTTP/1.1): TCP-Verbindung kann für weitere Austausche offen gelassen werden (Timeout, Connection: schließe Anfrage Header)
Caching: beim Client- und/oder Webproxy
Zuordnung Server-Host: 
- In HTTP/1.0 --> TCP Verbindung bestimmt Host
- In HTTP/1.1 --> Mehrere Hosts pro Server (Host in Anfrage spezifiziert)
![[HTTP Client Server.png]]
## Anfragen: Überblick
#### allgemeine Struktur
request = request-line (headerfield CRLF), CRLF, (message-body)
request-line = method SP request-uri SP HTTP-version CRLF
#### Kopfzeilenfelder
- bereitstellen zusätzlicher Informationen
- Parametrierung des Anfrageverhaltens
- Bsp.: Host, if_Modified_Since, User-Agent, Content-Length
#### Nachrichtentext
- enthält Ressourcendaten (MIME)
- kann weggelassen werden
#### Methodenarten
![[HTTP Methodenarten.png]]
beachte: zusätzliche Typen, die in Zwischenentwürfen definiert sind:
- PATCH, LINK, UNLINK, COPY, MOVE, WRAPPED
von einigen Servern unterstützt
## HTTP/1.1 Antworten Überblick
#### allgemeine Struktur
response = status-line (header-field CRLF), CRLF, (message-body)
status-line = HTTP-version SP status-code SP reason-phrase CRLF
#### Kopfzeilenfelder 
z.B. Accept-Ranges, ETag
#### Statuscode
3 stelliger Ergebniscode der die Antwortklasse spezifiziert ("404")
#### Phrase
für menschliche Benutzer bestimmt ("PAGE NOT FOUND")
![[HTTP Statuscodes.png]]
Bsp.:
- 100 weiter
- 200 ok
- 304 dauerhaft verschoben
- 400 ungültige Anfrage
- 500 Interner Serverfehler
## HTTP/1.1 Caching
__Cacheeintrag__ ist fresh, bis Ablaufzeit erreicht (Expires oder max-age Header Felder, sowohl Client als auch Server können diese Regel überschreiben (z.B. no-cache))
__Revalidierung veralteter Einträge__ mit dem Server (oder reload) (Basierend auf Änderungsdatum oder Entitäts-Tag (ETAG), bedingte Anforderungen: Headerfeld, um anzugeben, dass Anfrage nur ausgeführt werden soll, wenn Bedingung wahr ist (z.B.: If Modified-Since))
## HTTP Beispiel
![[HTTP Beispiel.png]]
grün ist user input, rot ist server output
