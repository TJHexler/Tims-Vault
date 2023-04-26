---
tags: Uni Syskon
---
# Middleware
## was ist Middleware
Middleware ist eine Art von Software, die zwischen verschiedenen Anwendungen, Systemen oder Netzwerken vermittelt. Sie dient als Vermittler, der Kommunikation, Datenübertragung oder Transaktionen zwischen verschiedenen Komponenten vereinfacht und standardisiert. Middleware kann auf verschiedenen Ebenen arbeiten, wie beispielsweise auf der Betriebssystemebene, auf der Anwendungsebene oder auf der Netzwerkebene.

Ein Beispiel für Middleware ist ein Message Broker, der Nachrichten zwischen verschiedenen Anwendungen vermittelt. Ein anderer Beispiel ist ein Webserver, der Anfragen von Clients empfängt und sie an eine Anwendung weiterleitet, um eine Antwort zu erhalten.

Middleware bietet viele Vorteile, wie beispielsweise eine höhere Interoperabilität zwischen verschiedenen Systemen, eine verbesserte Skalierbarkeit und Flexibilität sowie eine einfachere Integration von neuen Anwendungen und Technologien.
## Aufgaben
- befindet sich zwischen Anwendung und [[Betriebssystem]]
- bietet mehr Funktionalitäten als das BS, von denen viele Anwendungen profitieren (Bsp.: Katenbank-Schnittstellen, Kommunikation mit entlegenen Stationen, Grafik (OpenGL, Renderware))
- WindowsXP bietet eigene RPC an, Solaris auch
## gemeinsamer Speicher - Konzept
- zu Beginn: gemeinsamer Speicher = effizienter Weg für Interprozesskommunikation (IPC) auf einem Rechner
- archaische Abstraktion: Speicheradressen und Wörter
- mehrere Kontrollflüsse greifen auf gleichen Datenpunkt zu --> Konsistenz? --> Sperrung/Synchronisation notwendig
Realisierung:
- ohne Speicherschutz:
	- jeder Prozess kann auf jeden Speicherort zugreifen --> nur Sperrung erforderlich
- mit Speicherschutz:
	- geteilte physische Speicherseite muss virtuellem Adressraum kommunizierender Prozesse zugeordnet werden
	- physische Einzelkopie erfordert Sperrung
## verteilter gemeinsamer Speicher
- gleiche Philosophie: Speicherseiten teilen
- Hauptunterschied: kein gemeinsamer physischer Speicher
- erfordert explizite Kommunikation
- kann im [[Betriebssystem]] integriert werden: Demand Paging analog Seitenfehler
- erfordert Sperrung
- mehr Synchronisation
- weniger Parallelität
- --> schlecht Skalierbar
- verteiltes Demand Paging:![[verteiltes Demand Paging.png]]
- direkte Programmierung des Speichers oft als archaisch angesehen
- keine Datentypen und Typsicherheit
- Tupleräume abstrahieren konkreten Speicher und stellen Datentypen zur Verfügung
- Linda: Tupleraum-Pionier, in, out Operationen, Definition von Vorlagen (Wildcards für den Zugriff)
- JavaSpaces: Objekte in Datenpool, in, out Operationen, Vorlagen als Objekte
- trotz höherer Abstraktion bleiben Grundprobleme verteilter gemeinsamer Speicher: __Konsistenz & Synchronisation__
## Sockets
- Application Programming Interface(API), Protokollunabhängig, bieten 2 Arten von Diensten an:
	- verbindungsorientiert (zuverlässiger Datenstrom)
	- verbindungslos (Best-Effort, Nachrichtenaustausch)
- Grundlage für viele Middleware-Systeme
## Nachrichtenwarteschlangen
- Austausch von Nachrichten zwischen Prozessen
- Entkopplung der Kommunikation durch Warteschlangen
- lokale Interaktion mit Warteschlangen (Datenbank für Nachrichten)
- Warteschlangen speichern Nachrichten persistent (über Lebensdauer des Prozess) und synchronisieren sich gegenseitig
- asynchron, entkoppelt die Aktivierung beteiligter Prozesse
- ABER: Nachrichtenabstraktion - Bruch mit lokaler Programmstruktur
- Anwendungsbeispiel Banking: 
	- Tagsüber: Buchung und Befüllung der Warteschlangen
	- Nachts: Buchungstransaktionen ausführen - Leeren der Warteschlangen
- moderne Anwendungen: Sicherstellen von Konsistenz bei verteilter Koordination (eventually consistency)
- Bsp.: MQSeries (IBM)
## Events
Motivation:
- Client/Server Interaktion Anfrage/Antwort-basiert
- ein Client und ein Dienst kommunizieren (Synchron, 1:1, eng gekoppelt: Client und Dienst sind während des Kommunikationsvorganges aktiv, d.h. gleichzeitig laufende Prozesse)
ABER:
- oft leichtgewichtig
- unidirektionaler Mechanismus der außerdem 1:n Kommunikation ermöglicht wünschenswert
- genereller Mechanismus, Informationen werden asynchron über Events ausgetauscht (sehr oft verwendet z.B. Interaktion in GUIs, Austausch kann durch Nachrichten über TCP oder UDP erfolgen)
![[Events Middleware.png]]
Rollen: Supplier (stellt Event bereit), Consumer (verarbeitet Event)
Modelle: Push(Supplier stellt dem Consumer das Event bereit), Pull(Consumer holt sich das Event beim Supplier)
## Newsticker Beispiel
Verbraucher will über Änderung des Inhalts des Anbieters informiert werden und möglicherweise auf den Content an sich zugreifen
sporadische Änderungen, nicht festgelegte Änderungsrate
Kommunikation: 1:n ([[Multicast]])
Implementierungsoptionen:
- Callbacks
- Periodic polling
![[Supplier Consumer.png]]
## Monitoring
- [[Monitor]] sammelt Informationen
- Kommunikation: n:1 (periodisches Polling, asynchrone Benachrichtigung("Papier nachlegen"))
![[Monitoring.png]]
## Realisierung des Push/Pull-Modells
- Supplier und Consumer "müssen sich kennen"(Austausch von Objektreferenzen)
- keine Entkopplung bei der Aktivierung: gegenseitige Registrierung erforderlich
- Lösung: Event-Kanal (vgl. Nachrichtenwarteschlangen)
![[Event-Kanal.png]]
## Event-Kanal
- stellt Events bereit
- Modell (push/pull) abhängig von individuellem Consumer oder Supplier
- der Event-Kanal kann Persistenz, Einhaltung der Reihenfolge, Historie, Zeitbeschränkung ermöglichen (aber muss nicht)
![[Event-Kanäle.png]]
### Bsp.: COBRA Event Dienst
- unterstützt die vorgestellten Konzepte
- Zugang zum Event-Kanal über proxy-Objekte (Stellvertreterobjekte)
	- Push Event Kanal --> Consumer: Consumer muss das Objekt bereitstellen (Callback)
	- Pull Ebent Kanal --> Supplier: Event Kanal muss Event buffern, muss Consumer regelmäßig abfragen --> Netzwerklast
- typisiert (erfordert generierte Vorlagen) und nicht typisierte Events (beliebiger generische Datencontainer)
## Publisher/Subscriber Systeme
Interaktion:
- Subscriber interessiert sich für Events eines bestimmten Typs
- Publisher gibt Events aus 
Themenbasiert (kanalbasiert): 
- ähnlich zu Events
- jedes Event wird durch einen Publisher in einem Kanal veröffentlicht
- Subscribers abonnieren bestimmte Kanäle
Inhaltsbasiert:
- Adressierung nach Themen/Inhalten
- keine Kanäle
- abonnieren über beliebige Abfrage des Inhalts des Events
Publisher und Subscriber sind entkoppelt
n:m Kommunikation
Anwendungsbeispiel: Aktienticker
Bsp.: TIBCO Information Bus
## mobile Agenten
Agent:
- Software, die im Namen eines Benutzers handelt
Mobile:
- Agent migriert autonom zu einem anderen Ausführungshost
Bisher:
- Daten an festen Ausführungscode gesendet (Client sendet Anforderung, Server verarbeitet sie)
Agenten:
- Daten und/oder Code werden an Ort ihrer Ausführung gesendet
mögliche Anwendungsszenarios:
- "Shopping"-Agent: migriert entlang potenzieller Geschäfte und sammelt Angebote, spart Bandbreite für den Client
- Netzwerk-Management-Agent: kann isoliert von Management-Software arbeiten, z.B. in verschiedenen Netzwerkpartitionen
- Kapselung von Richtlinien: in der allgegenwärtigen Datenverarbeitung bewegen sich Nutzer auf unterschiedlichen Domains, der Agent kann dem User folgen und diesen repräsentieren (Richtlinien, Geldbörse, etc.)
- Schadsoftware: Würmer
Eigenschaften:
- hochverteilt und dynamisch
- Agenten entscheiden autonom, wann und wo migriert werden soll
- keine Software-Engineering-Methodik bildet dies ab (bisher)
- Lösung auf der Suche nacgen Problem
- Bsp. Mole, Grasshopper
## Multimedia
bisher: diskrete Daten
Multimedia: kontinuierliche Daten (Audiostream, Videostream, "Lip-Synchronisation")
Anwendungsspezifische Fehlerkorrektur (Verlust eines Bildes besser als Verzögerung während der Wiedergabe)
Infrastrukturen, in der Regel eng mit Anwendungen gekoppelt
Anpassungen der erforderlichen Anwendungen (z.B. Bandbreite)
## Remote Procedure Call (RPC)
- klassische Middleware
- Ziel: gleiche Abstraktion für lokale und entfernte Interaktion
- synchrones Kommunikationsmodell
- soll Verteilungstransparenz herstellen
	- entfernte Interaktion ähnelt lokaler Interaktion
	- viele Aspekte: Migration, Ausführungsort, Aufruf, Binden, etc.
- Dienstspezifizierung (Interface Definition Language, IDL oder bestehende Schnittstellendefinitionen, bspw. Klasse)
- Daten mit Konvertierungsinformation transportiert (marshalling)
- ABER: Verteilungstransparenz erreichbar?
	- Laufzeit, Verzögerung
	- Fehler
	- Call by reference
- Bsp.: Distributed Computing Environment (DCE), Sun RPC, gRPC, ICE, etc.
Architektur:
![[RPC Architektur.png]]
![[Remote Procedure Call.png]]
### was ist ein remote procedure call?
Ein Remote Procedure Call (RPC) ist ein Protokoll, das es einer Anwendung ermöglicht, eine Funktion oder Methode auf einem entfernten Computer oder einer entfernten Netzwerkumgebung aufzurufen, als ob sie auf dem lokalen Computer ausgeführt würde. Dies ermöglicht es Anwendungen, auf entfernte Ressourcen zuzugreifen und Remote-Dienste nahtlos in ihre Anwendungen zu integrieren.

Das RPC-Protokoll besteht aus mehreren Schichten und arbeitet typischerweise auf der Transportebene. Das bedeutet, dass es ein Transportprotokoll wie TCP oder UDP verwendet, um die Daten zwischen den Computern zu übertragen. Die RPC-Schicht verwendet dann ein bestimmtes Protokoll, um die Parameter der Remote-Funktion zu übergeben und das Ergebnis zurückzugeben.

Ein Beispiel für die Verwendung von RPC ist eine Anwendung, die eine Datenbank auf einem entfernten Server verwendet. Die Anwendung kann eine Funktion aufrufen, die vom Server bereitgestellt wird, um Daten von der Datenbank abzurufen oder zu aktualisieren. Der RPC-Mechanismus ermöglicht es der Anwendung, die Funktion als Teil ihrer lokalen Anwendungslogik aufzurufen, ohne sich um die Details der Netzwerkkommunikation kümmern zu müssen.

RPC wird häufig in verteilten Systemen, Cloud-Computing-Plattformen und Webanwendungen eingesetzt, um den Zugriff auf entfernte Ressourcen zu vereinfachen und die Entwicklung von Anwendungen zu erleichtern.

### Remote Method Invocation (RMI)
- RPC imperatives Konzept
- Objektorientierte-Sprachen sind beliebt
- Objektorientiertheit stellt Client/Server-Modell kanonisch dar
- ähnliche Abstraktion wie RPC für Objekte gewünscht
- Bsp.: COBRA, DCOM, Java/RMI
#### was ist eine remote method invocation?
Remote Method Invocation (RMI) ist ein Mechanismus in der Programmierung, der es Anwendungen ermöglicht, Methoden auf entfernten Objekten oder Servern auszuführen, als ob sie lokal auf dem eigenen Computer ausgeführt würden. RMI ist eine Erweiterung des Remote Procedure Calls (RPC) und ermöglicht es, Objekte und Methoden zwischen verschiedenen Java Virtual Machines (JVMs) zu übertragen.

RMI verwendet das Java Remote Method Protocol (JRMP), um die Kommunikation zwischen Client- und Serveranwendungen zu erleichtern. Der Client ruft dabei eine Methode auf einem entfernten Server auf und erhält das Ergebnis zurück, als ob die Methode lokal ausgeführt worden wäre.

Ein Beispiel für die Verwendung von RMI ist eine verteilte Anwendung, bei der die Anwendungslogik auf mehrere Server verteilt ist. Ein Client kann dann eine Methode auf einem entfernten Server aufrufen, um Daten abzurufen oder zu aktualisieren. Die Anwendungsentwickler können dann die RMI-Mechanismen verwenden, um die Kommunikation zwischen den Servern und dem Client transparent zu gestalten.

RMI wird hauptsächlich in Java-basierten verteilten Anwendungen, wie beispielsweise Enterprise-Anwendungen, verwendet. Es ermöglicht es, die Komplexität der verteilten Systeme zu reduzieren und die Entwicklung von Anwendungen zu erleichtern, indem es die Abstraktion von entfernten Objekten und Methoden bereitstellt.
#### Beispiel
Entwicklungsschritte:
- Schnittstellenbeschreibung (IDL) bereitstellen
- IDL in Zielsprache übersetzen
- hinzufügen von Client/Service-Code
- Client/Service kompilieren, ORB binden
- ausführen
Beispiele für COBRA in C und für Java RMI in Java bei K6.38-55

### was passiert? (Client-Side)
![[Client Side Ablauf.png]]
Skelett = Vorlage für den Service, generiert von IDL
Service erbt Skelettverhalten und fügt Service-Implementierung hinzu
### Future RPC
- Entkopplung der Synchronisierung mit zukünftigen Ergebnis des entfernten Aufrufs
- Future Objekt wird nach jedem Aufruf auf Clientseite instanziiert
- Der Client ist nicht blockiert und kann auf die Antwort zugreifen, wenn sie verfügbar ist, oder blockiert bei Zugriff
![[Future RPC.png]]
### Aufrufsemantik
Was passiert bei Fehlern in der Kommunikation?
- lokale Aufrufe werden genau einmal ausgeführt
- nicht möglich mit entferntem Aufruf
#### 4 Aufrufsemantiken
##### Maybe
- Absender sendet Nachricht erst einmal
- keine Garantien über die Zustellung
Client stub: 
- sendet Auftrag & startet Timer
- bei Timeout: Exception auf Client Seite werfen
- Zustand des Aufrufs nicht definiert
server stub:
- keine Erkennung von Duplikaten
- sendet Ergebnis nach Bearbeitung des Aufrufs
![[Maybe Aufrufsemantik.png]]
##### At least once
- Absender wiederholt Senden, bis die Bestätigung empfangen wird
Client stub:
- sichert Aufruf lokal
- sendet Aufruf periodisch (nach Timeout) bis Ergebnis vorliegt
- löscht Aufruf, wenn Ergebnis vorliegt
server stub:
- keine Erkennung von Duplikaten
- sendet Ergebnis nach Bearbeitung des Aufrufs
- ![[At least once Aufrufsemantik.png]]
##### At most once
- Absender sendet Nachricht nur einmal
- überprüft ob Nachrichten vor dem Senden noch nicht zugestellt wurden
client stub:
- sichert Aufruf lokal
- sendet Aufruf periodisch (nach Timeout) bis Ergebnis vorliegt
- sendet ACK wenn Ergebnis empfangen
- löscht Aufruf, wenn Ergebnis vorliegt
server stub:
- Duplikaten-Erkennung auf Basis der Aufruferkennung
- sichert Ergebnis nach Bearbeitung
- sendet Ergebnis periodisch bis ACK empfangen
- löscht Ergebnis nach empfangenem ACK
Ausführung kann bei Client oder Server Fehlern nicht garantiert werden
![[At most once Aufrufsemantik.png]]
##### Exactly once
- Absender wiederholt Senden, bis Bestätigung empfangen wird
- Empfänger stellt sicher, dass Nachricht genau einmal zugestellt wird
das selbe Protokoll wie at-most-once aber:
- Aufträge und Antworten werden auf stabilen Speicher geschrieben
- save und unsave sind atomare Operationen
- Ein Fehler des Servers vor Sichern(save) setzt Interaktion zurück (rollback)
client recovery:
- Auftrag in stabilem Speicher
- Auftrag wird periodisch gesendet bis Ergebnis vorliegt
server recovery:
- Antwort in stabilen Speicher
- Antwort wird gesendet bis ACK empfangen wird
Bsp.:
- wenn ihnen jmd. Geld zahlt, wollen Sie, dass es "at least once" ist
- wenn Sie jmdn. Geld zahlen, wollen Sie, dass es "at most once" ist
![[Exactly once Aufrufsemantik.png]]
### Parameterübergabe
Daten können mit verschiedenen Semantiken übergeben werden
Semantik der Parameterübergabe
- Call by value
- Call by reference (remote-adressraum lokale Referenzen können nicht funktionieren)
copy/restore:
- ähnlich zu call by reference
- ähnliche Semantik
- call by value zu Übergeben von Parametern und lokalen Verweisen auf diese Kopien verwendet
- Speichermanagement wird umständlich
	- sperren oder Referenzzählung zur Vermeidung von Nebenwirkungen
	- Weitergabe einer Referenz von Aufrufer --> Aufgerufenen --> Aufrufer und jewels Freigabe der Referenz bei Weitergabe
- komplexe Datentypen (Bäume, Listen) führen zu Kopien
## kleine Zusammenfassung
Middleware
- bietet eine Vielzahl von möglichen Abstraktionen
- Standards können einheitliche Abstraktion für Anwendungen sicherstellen
- abstrahiert von unterschiedlichen [[Betriebssystem]]en/Plattformen
- erleichtert den Datenaustausch und den Aufruf von Diensten
Die Wahl von Abstraktion und Middleware ist abhängig von 
- Anwendungsanforderungen
- bestehenden Plattformen, Sprachen
- Fähigkeiten von Designern und Programmierern