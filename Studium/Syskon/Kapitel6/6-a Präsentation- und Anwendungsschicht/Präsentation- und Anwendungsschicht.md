---
tags: Uni Syskon
---
# Präsentation- und Anwendungsschicht
#### Motivation
wie sieht Layer 7 [[Präsentationsschicht]] für die Anwendung aus? - kann unterschiedlich sein (vgl. [[Middleware]]), wie interagieren Anwendungen?
--> __Protokolle__
#### Wiederholung
Layer 6: welche Daten werden ausgetauscht? - Daten und ihre Repräsentation (bits, bytes, structs, books, etc.)
Layer 7: wie werden Daten ausgetauscht? - Interaktionsmuster
Bsp.: add(5,4) --> send ("add", 5, 4, return to address)
## SMTP (simple Mail Transfer Protocol)
Ziel: mails zuverlässig und effizient versenden
standard definiert in RFC 821
Format (Internet Message Format) definiert in RFC 822
#### Aufbau
Umschlag (Envelope)(von MTAs verwendet) - die Serverkomponente, die E-Mails austauscht
Header (von MUAs verwendet) - Ihr bevorzugter E-Mail-Client
zusätzliche Header können verwendet werden (X-...)
Leere Zeile
Nachrichtentext (7-Bit ASCII)
![[SMTP.png]]
![[SMTP Beispiel.png]]
Beispiel Session:
![[SMTP Beispiel Session.png]]
#### Probleme
- Nachrichtenlänge auf 64 kb begrenzt
- es dürfen nur 7-Bit ASCII-Zeichen verwendet werden
- keine Authentifizierung
- Mailstorms (unendliche Schleifen)
- Timeouts
#### Verbesserungen
- ESMTP (Extended SMTP)
- SMTP AUTH
- MIME (Multipurpose Internet Mail Extensions)
## [[Middleware]] Application Layer
Für einen Remote-Methodenaufruf muss:
- Dienst adressiert werden (object reference)
- die Parameter konvertiert werden (presentation Layer)
- Anfrage- u. Antwortnachrichten modelliert werden
### Interoperable Objektreferenzen (IOR)
Objektreferenzen identifizieren Objekte
Für Remoteobjekte gibt Objektreferenz an:
- Objekt ist null
- Objekttyp
- unterstützte Protokolle für den Zugriff auf das Objekt
### Interoperabilitätsprotokoll
Transport und Präsentation:
- ermöglichen Datenaustausch zwischen entfernten Stationen
Interoperabilitätsprotokoll: 
- basierend auf L4 (oft Streams)
- definiert Nachrichten als Protokolldateneinheiten (PDUs)
- entkoppelt technische Bereiche, z.B. die Kommunikationsstationen
- spiegelt Methodenaufrufsemantik in Nachrichten wieder
### Interoperabilitätsprotokoll für RMI
Methodenaufruf --> Server/Client Modell
Aufruf initiieren --> request()
Ergebnis übertragen --> reply()
synchrones Kommunikationsschema
## Protocol Data Unit (PDU)
- PDUs definieren Nachrichtenaustausch
- allgemeines Inter-ORB-Protokoll/Internet Inter ORB-Protokollbeispiele von CORBA
- Remote Methodenaufruf (Anfrage PDU, Antwort PDU)
- generell:
	- Header: identisch für beide
	- Body: enthält PDU-spezifische Informationen
#### Anfrage/Antwort
![[Anfrage und Antwort PDU.png]]
- VN Version
- BO Byte Order --> Bytes von links nach rechts oder anders herum lesen?
- MT Message Type
- MS Message Size
#### PDU Nachrichtenheader
IDL Definition: Zuordnung zum Bytepuffer(CDR)
![[PDU Nachrichtenheader.png]]
#### PDU Anfragenheader
![[PDU Anfragenheader.png]]
- RequestID: Zuordnen von Antworten zu Anfragen
- object_key: lokale Objektadresse am Remote-Standort (Teil der Objektreferenz)
- Operation: Name der aufzurufenden Methode
#### PDU Anfragebody
Objekt ist wohldefiniert:
- ORB = Empfänger von PDU
- Transportendpunkt basierend auf Informationen aus Referenz
- lokale Adresse des Objekts: object_key
Operation wohldefiniert durch Schnittstelle:
- Anzahl und Typen von Parametern
- Anfrage Body enthält codierte Parameter
#### PDU Antwort Header
![[PDU Antwortheader.png]]
Replystatus: Request Ok oder Exception
Replybody: Ergebnisparameter oder Exception

## kleine Zusammenfassung
- Anwendungsschichtprotokolle sind i.d.R. anwendungsspezifisch
- Wiederverwendung möglich (MIME Typen fpr SMTP und [[HTTP]], TELNET in FTP wiederverwendet)
- [[HTML]]
- generische Application Layer Protokolle für die Interoperabilität von [[Middleware]]
	- standardisieren Nachrichten
	- spiegeln Interaktionsmodell der Anwendung wieder
	- basieren auf bekannten Datenrepräsentationsarten