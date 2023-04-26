---
tags: Uni Syskon
---
# Das OSI Referenzmodell
auf Grundlage eines Vorschlags der ISO (International Standart Organization): __Standartisierung der Protokolle auf Schichten und Beziehungen der Schichten__

OSI = Open Systems Interconnections
Modell mit 7 Schichten
![[OSI Referenzmodell.png|500]]
## Application (Anwendung)
- Manifestiert für jeweilige Anwendung relevanten Meldungen und Daten
## Presentation
- Transformiert Anwendungsdaten zwischen verschiedenen lokalen Darstellungen (Host, Sprache)
## Session
- verwaltet Sitzungsstatus der einzelnen Verbindungen 
- z.B. Sicherheitszuordnungen
## Transport
- ermöglicht Kommunikation zwischen Prozessen 
- Adressierung lokaler Stationsprozesse
- verschiedene Servicetypen:
	- verbindungslos: datagram
	- verbindungsorientiert: zuverlässig, stream
## Network
- ermöglicht Kommunikation zwischen beliebigen Stationen
- Adressierung von Stationen
- Austausch von packets (Paketen)
- best-effort-service
## Data link (Sicherung)
- Verbindung zweier Stationen
- Austausch von frames (Rahmen)
- Zugang zum Übertragungsmedium (media access control - MAC)
- Fehlerbehandlung
- Flußkontrolle
## Physical (Bitübertragung)
- Verbindung zweier Stationen
- Übertragung & Austausch physischer Signale
## Kritik
- schlechtes Timing
- schlechte Technologie
- fehlerhafte Implementierung
- schlechte Politik
- [[TCP IP]] war da und hat bereits funktioniert