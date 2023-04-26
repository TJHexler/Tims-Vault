---
tags: Uni Syskon
---
# Referenzmodelle
## [[OSI]]
## [[TCP IP]]
## Verwendung von Protokoll-Stapel (protocol stacks)
in der Regel besteht eine klare Trennung zwischen generisch und anwendungsspezifischen Diensten:
	- generisch: Routing, Ablaufsteuerung, physikalisch
	- anwendungsspezifisch: Datencodierung (Präsentation), Kommunikationsmodell
[[Betriebssystem]] bietet in der Regel Programmierabstraktionen bis Programm-Layer vier (L4)

## Dienste für Anwendungen (L4)
![[Layer 4.png]]

## Dienstprimitive
- Menge von Basisdiensten (primitives)
- Dienste werden durch Kombinationen der Primitives realisiert
- oft parametriert
![[Dienstprimitive.png]]
![[Dienstprimitives im Einsatz.png]]

## Layer 4 - Transport Internet Protokolle
- Die Transportschicht des Internet besteht aus 2 Protokollen:
### UDP (User Datagram Protocrol) verbindungsloses Protokoll
- unzuverlässig --> Nachrichten können verloren gegen
- ungeordnet --> Reihenfolge der Nachrichten bei Versand und Erhalt ggf. unterschiedlich
- leichtgewichtige Realisierung --> kein Verbindungszustand, Nachrichten nicht nummeriert, etc.
- Abstraktion: Diagramme --> Packets werden komplett versendet, keine Fragmentierung
### TCP (Transmission Control Protocol) verbindungsorientiertes Protokoll
- stellt Verbindung vor Kommunikation her
- zuverlässig --> Sicherheit, dass Nachricht am Ziel ankommt
- Fehlerbehandlung
- geordnet --> Reihenfolge bei Versand und Erhalt gleich
- Overhead/Aufwand --> Nachrichtenverwaltung, Informationen zur Reihenfolge, Status
- Abstraktion: Streams --> Daten werden aus Strom gelesen. Strom besteht aus Segmenten, die für Nutzer der Schicht nicht sichtbar sind
## Sockets
- Netzwerkschicht adressiert Station (Computer) nicht die Anwendung (Email, WWW, etc.)
- TCP und UDP nutzen das Port Konzept (indirekte Adressierung):
	- Port ist "Lieferort" für Transport Layer (Identifiziert durch eine Zahl: 0-65535)
	- typisiert (TCP oder UDP)
- Sockets verbinden Anwendungen mit Protokollsoftware um einen Prozess mit einem Port interagieren zu lassen
- Sockets sind eine API (application programming interface) zwischen Anwendungen und Protokoll-Stack
- [[TCP IP]] standardisiert keine API: 
	- Hintergrund: Annahme, dass keine API auf alle Anwendungen passt
	- ABER: Sockets sind weit verbreitete API - auch für TCP/IP
- primitives für TCP Sockets:
![[primitives für TCP Sockets.png]]

Java Server, Client bei K5.63

## TCP Sockets
![[TCP Sockets.png]]
## UDP Sockets
![[UDP Sockets.png]]

## mini Wiederholung
- [[verteilte Systeme]] basieren auf Computernetzwerken
- grundlegende Dienste in Layer 4: Datagram, Ströme
- komplexe Konzepte für Synchronisation, Fehlertoleranz und Skalierbarkeit
- Programmierung mit Sockets bricht Abstraktionen zu lokalen Programmstrukturen (Objekte, Methoden)
- [[Middleware]]-Konzepte erforderlich/hilfreich