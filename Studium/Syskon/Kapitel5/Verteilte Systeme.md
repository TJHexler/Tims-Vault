---
tags: Uni Syskon
---
# verteilte Systeme
## Eigenschaften
- Knoten/Hosts (Computersysteme, verschiedene [[Betriebssystem]]e, unterschiedliche Hardware und Ressourcen)
- Kanten: Computer Netzwerk (Protokolle([[TCP IP]], UDP/IP, X25, etc.); Medien (IEEE, Bluetooth, Ethernet, etc.))
- einzelne Fehlerpunkte, Leistungsengpässe
- keine globale Ansicht, keine globale Zeit
- heterogen  Netzwerk und Knoten
ABER
- Ressourcenfreigabe möglich (Drucker, CPU, etc.), verbindet entfernte Orte, Redundanz --> Fehlertoleranz u,d Skalierbarkeit, spiegeln Organisationsstruktur wieder
## Anforderungen
viele mögliche Schwierigkeiten
unterschiedliche Nutzungsarten, Systemanforderungen, interne Probleme (nicht synchronisierte Uhren, etc.), externe Bedrohungen
--> komplexe Vorsichtsmaßnahmen nötig
Design verteilter Systeme muss beachtet werden: Architekturmodelle, Interaktionsmodelle, Ausfälle in verteilten Systemen, Sicherheitsmodelle
## Modelle
### Architekturmodell
- definiert die Struktur verteilter Systeme mit verschiedenen Komponenten
- zwei wichtige: __Multi-Tier, Peer-to-Peer__
- abstrahiert die Funktionen der einzelnen Komponenten unter Berücksichtigung
	- der Komponentenplatzierung im Computernetzwerk, um [[Muster]] für die Daten- und Workloadverteilung zu definieren
	- der Zusammenhänge zwischen Komponenten, der Identifizierung von Rollen und Kommunikationsmustern
	- Interaktion ist der Schlüssel für verteilte Architekturen
### Interaktionsmodelle
- bestehen aus Rollen und Interaktionen
- Rollen bestimmen den Kommunikationspartner
- Interaktion definiert Daten die ausgetauscht werden sowie das Synchronisationsmuster
### Producer/Consumer Modell
Producer: 
- generiert Daten und sendet diese an Consumer
- Interaktion: __unidirektionale Kommunikation__
Consumer:
- erhält und verarbeitet Daten
Bsp.: VideoStream von Kamera wird an Person gesendet, die Stream schaut
### Pipeline Modell
![[Pipeline Modell.png]]
__unidirektionale Kommunikationskanäle__
zwischen Prozesse sowohl Producer als auch Consumer
Bsp.: Datenaustausch zwischen Partner in der Zulieferungskette
### Client-Server Modell
Client sendet service request an Server, __aktive Einheit__
Server wartet auf Anfrage, verarbeitet sie, sendet Ergebnis zurück an Client, __passive Einheit__
![[Client-Server Modell.png]]
### Client-Server Architekturen
Service kann durch verschiedene Server Prozesse implementiert werden
- Daten und/oder Funktionen können auf mehreren Knoten verteilt und/oder repliziert werden
- Server ändert Rolle zu Client, um Funktionen von anderen Servern anzufordern
Bsp.: Suchmaschinen (Index partitioniert und repliziert - Domain Name System-Verzeichnis verteilt und repliciert)
![[Client Server Architektur.png]]
### Multi-Tier Architektur
- Client/Server entspricht nicht (notwendigerweise) der Anwendungsstruktur
- Platzierung und Relevanz von Komponenten entscheidend (Fehlertoleranz, Leistungsengpässe)
- Ansatz: allg. Architekturmodell (Aufteilung der Anwendungen in größere Komponenten, Benutzerinteraktion, Workflow, Datenspeicher)
Präsentationsebene:
- Interaktion mit Benutzer
- in der Regel eine Rolle in einem Workflow
- Absturz begrenzte Wirkung
Verarbeitungsebene:
- realisiert Workflow
- bedient Reihe von Präsentationsebenen
- repräsentiert Einheiten der Organisation
- Absturz wirkt sich auf das Geschäft einer Abteilung aus
Datenbank-Speicherebenen:
- persistente Datenspeicherung
- in der Regel unternehmensweit (umfasst mehrere Abteilungen)
- Crash wirkt sich auf alles aus
![[Multi-Tier Architektur.png]]
Use Cases: SAP Net Weaver, Enterprise JavaBeans
### Peer-to-Peer
anderer Anwendungsbereich, anderer Ansatz:
- keine Anforderung an zentral verwaltete Server
- Bereitstellung von Ressourcen (Daten, Speicher, Bandbreite) durch jeden Peer
- --> Gesamtkapazität des Systems steigt mit Anzahl der Peers
- alle Teilnehmer gleichberechtigt (anders als Client/Server Modell)
- Anwendungen: Datenaustausch, Kommunikation, Entertainment
Hybrid Peer-to-Peer:
- Server für Peer-Koordination verwendet
- Peers lassen Server wissen, welche Ressourcen gemeinsam verwendet werden
- direkte Interaktion zwischen Peers
- Bsp.: Skype, Spotify
![[Hybrid Peer-to-Peer.png]]
Pure Peer-to-Peer
Peers alle gleichberechtigt
kein Server --> jeder Peer fungiert als Client und Server
Herausforderung: Verteilung und Lokalisierung von Daten und Ressourcen
![[Pure Peer-to-Peer.png]]

## Netzwerkarchitekturen verteilter Systeme: Layered Networks
Problem: Design kommunikativer Systeme ist komplex (physische Übertragung, Fehlerkorrektur)
Lösung: Mehrschichtige Architekturen (Layered Systems):
- jede Schicht realisiert Ebene der Abstraktion 
- Schnittstellen: Servicebereitstellung einer Schicht für die darüberliegende /Einkapselung
- Protokolle: Kommunikation zwischen zwei Parteien desselben Layers auf verschiedenen Maschinen (Nachrichten, Regeln)
Grundidee:
![[Layered Network Grundidee.png]]
![[Layered Network.png]]

### Protokoll
- Kommunikationsvereinbarung zwischen 2 Parteien des gleichen Layers auf verschieden Maschinen
- bestehen aus __Nachrichten und Regeln__
- Nachrichten bestimmen Inhalt der Interaktion, hängen vom Anwendungszweck ab 
- Regeln bestimmen Beziehung zwischen Nachrichten (z.B.: Login Message before Password Message)
### Schnittstelle
- definiert welche Service primitives die untere Ebene der darüberliegenden bereitstellt (Interfaces bieten Funktionalität von Layer k, Layer k+1 an)
- Aufruf einer Schnittstelle ist oft Auslöser einer Protokollnachricht (z.B.: connect/accept, read, write)
- Nachrichten der Anwendungsschicht werden als Nutzlast/payload von Nachrichten auf Schicht 4 gesendet ( write(server,"Bombe" + X + Y); --> Resultat: "Bombe:" + X + Y wird gesendet)

