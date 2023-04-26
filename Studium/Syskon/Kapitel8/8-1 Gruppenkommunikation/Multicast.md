---
tags: Uni Syskon
---
# Gruppenkommunikation
Verwendung von Kopien/[[Replikation]]en kann Zuverlässigkeit und Fehlertoleranz erhöhen. Bedingt zuverlässige Zustellung von Nachrichten und Reihenfolge an die Kopien (Konsistenz) --> Konsistenzkonzepte arbeiten mit Begriff __Zeit__ (physisch oder logisch), __Multicastkommunikation__ um Nachrichten in Reihenfolge an [[Replikation]]en zu senden
# IP Multicast
- einfache Implementierung der Gruppenkommunikation im Netzwerk
- baut auf IP auf
- erlaubt Sender einzelnes IP-Paket zu Menge von Computer zu senden (__Multicast-Gruppe__)
	- D-Klasse Internet Adresse mit ersten 4 Bits 1100
- dynamische Gruppenmitgliedschaft
	- senden an Gruppe geht mit und ohne Mitgliedschaft
- zum multicasten wird UDP datagram mit Multicast Adresse gesendet
- Beitritt:
	- Socket join(s.joinGroup(group)) --> Nachrichten an Gruppe können erhalten werden 
- Multicast Router:
	- lokale Nachrichten nutzen lokale Multicast-Kapazität
	- machen das effizient, weil sie andere Router auf Weg auswählen
- Ausfallmodell:
	- Auslassungsfehler (nicht alle Mitglieder erhalten Nachrichten, z.B. Empfänger kann Nachricht nicht droppen, oder Multicast-Router versagt)
- IP-Pakete können in falscher Reihenfolge ankommen --> Gruppenmitglieder können Nachrichten in unterschiedlicher Reihenfolge erhalten
# Multicast
- Kommunikation erfordert Koordination und Einigung
- Ziel der Gruppenmitglieder: Kopien erhalten, was an Gruppe gesendet wurde
- unterschiedliche Zustellgarantien: Einigung auf bestimmte Menge empfangener Nachrichten oder auf eine Empfangsreihenfolge
- Prozess kann multicasten indem er einzelne Operation nutzt, statt an alle Mitglieder zu senden
	- Die Einzeloperation ermöglicht:
	- __Effizienz__: es muss nur einmal über jede Verbindung gesendet werden, über Hardware-Multicast wenn verfügbar, z.B. multicast von einem Computer in London zu 2 Computern in Peking
	- __Zustellungsgarantien__: Garantie nicht möglich, wenn multicast als mehrere Sendevorgänge implementiert ist und der Sender ausfällt kann Reihenfolge erstellen
## Systemmodell
- System besteht aus Menge von Prozessen, die zuverlässig über 1-1-Kanäle kommunizieren können 
- Prozesse sind nur durch Crashs fehlerhaft (keine byzantinischen Fehler --> siehe später)
- Prozesse sind Mitglieder von Gruppen - die Empfänger von Multicast-Nachrichten sind
- Prozesse können zu mehr als einer Gruppe gehören
- Operationen
	- multicast(g,m) sendet Nachricht m an alle Mitglieder in Prozessgruppe g
	- deliver(m) wird aufgerufen, um Multicast-Nachricht zu liefern. Die unterscheidet sich von receive da der Empfang verzögert werden kann, um korrekte Reihenfolge oder Zuverlässigkeit zu gewährleisten
- Multicast Nachricht m trägt die Kennung (__id__) des Sende-Prozesses __sender(m)__ und die id der Zielgruppe __group(m)__
- Annahme: keine Fälschung der Herkunft und des Empfängers der Nachrichten
## offene und geschlossene Gruppen
geschlossene:
- nur Mitglieder können an die Gruppe senden
- ein Mitglied liefert auch an sich selbst aus
- nützlich für Koordination von Gruppen kooperierender Server
offene:
- nützlich für Benachrichtigung über Events an interessierte Prozessgruppen
## Verlässlichkeit der 1-zu-1 Kommunikation
__Validität__:
- jede Nachricht im Nachrichtenausgangspuffer wird schlussendlich an Nachrichteneingangspuffer des/der Empfänger/s geliefert
- Verwendung von Bestätigungen und Wiederholungsversuchen
__Integrität__
- Empfangene und gesendete Nachricht sind identisch, keine Nachricht wird doppelt gesendet
- verwendet checksums
- lehnt Duplikate durch Nachrichtenkennungen (id) ab (z.B. durch Wiederholungsversuche)
## Basis Multicast
- korrekter Prozess wird Nachricht ausliefern, solange __Multicaster nicht crasht__ (IP Multicast garantiert das nicht)
- Primitive heißen B-multicast und B-deliver
- einfache (aber ineffiziente) Implementierung:
	- 1-1 (Unicast) send
	- __B-multicast(g,m)__ //für jeden Prozess p aus g: send(p, m)
	- __receive(m)__ //bei Prozess p: B-deliver(m) zu p
- Problem: wenn Anzahl der Prozesse hoch, leidet das Protokoll unter ack-implosion
## zuverlässiger Multicast
- Protokoll ist korrekt, auch wenn Multicaster crasht
- Operationen R-multicast und R-deliver werden bereitgestellt
__Integrität__:
- p aus group(m), m wurde einer multicast-Operation vom sender(m) zur Verfügung gestellt
- korrekter Prozess, p liefert m maximal einmal aus
- Integrität wie bei 1-1 Kommunikation
__Validität__:
- wenn korrekter Prozess m multicastet, wird er m auch schlussendlich ausliefern
- Vereinfachung in dem Initiator p als Prozess ausgewählt wird
__Einigung__:
- wenn korrekter Prozess m ausliefert, dann werden alle korrekten Prozesse der Gruppe group(m) m ausliefern
- "Alles oder Nichts" - Atomizität in der Gruppe der korrekten Prozesse, auch wenn der Multicaster crasht
### zuverlässiger Multicast: Algorithmus über Basis Multicast
- Prozesse können mehreren Gruppen angehören
Einigung:
- jeder korrekte Prozess B-multicastet die Nachricht an alle anderen
- wenn p nicht R-delivered dann, weil er nicht B-delivered da es sonst auch keiner tat
Integrität:
- da zuverlässige 1-1 Kanäle Integrität garantieren, die für B-multicast verwendet werden
Validität:
- korrekter Prozess wird an sich selbst B-delivern
![[zuverlässiger Multicast Algorithmus über Basis Multicast.png]]
### zuverlässiger Multicast über IP Multicast
- Protokoll nimmt geschlossene Gruppen an. Es nutzt: angehängte Bestätigungsmeldungen, negative Bestätigungen bei verpassten Nachrichten
- Prozess p verwaltet:
	- $S^p_g$: Eine Nachrichtensequenznummer für jede seiner Gruppen
	- $R^q_g$: Eine Sequenznummer der letzten Nachricht, die von dem Prozess q in Gruppe g erhalten wurde
- Prozess p sendet die Nachricht m an Gruppe g: R-multicast
	- hängt $S^p_g$ an Nachrichten und Bestätigungen für Nachrichten, die in der Form g,$R^q_g$ erhalten wurden, an
	- verwendet IP Multicast für Nachricht m an g, erhöht $S^p_g$ um 1
Verhalten beim Erhalt einer Nachricht an g mit S von p:
- wenn S = $R^p_g + 1$ R-deliver die Nachricht und erhöhe $R^p_g$ um 1
- wenn S $<= R^p_g$ verwerfe die Nachricht
- wenn S $> R^p_g$ oder wenn R < $R^p_g$ (für ack q,R), dann wurden Nachrichten verpasst und sie werden mit negativer Bestätigung angefordert. Neue Nachricht kommt in Warteschlange, um später geliefert zu werden
### Die Warteschlange für aufkommende Multicast-Nachrichten
- vereinfacht das Protokoll, Sequenznummern können Mengen von Nachrichten repräsentieren
- Warteschlangen werden auch für Ordnungs-Protokolle verwendet
![[Warteschlange Nachrichten Multicast.png]]
## Eigenschaften zuverlässiger Multicasts über IP
__Integrität__:
- doppelte Nachrichten werden erkannt und aussortiert
- IP Multicast nutzt Checksums um korrupte Nachrichten zu erkennen
__Validität__:
- durch IP-Multicast, bei dem Sender auch an sich selbst sendet
__Einigung__:
- Prozesse können fehlende Nachrichten identifizieren
- Kopien der gelieferten Nachrichten mpssen verwahrt werden, um sie an andere ebenfalls zu vermitteln
## geordneter Multicast
- grundlegender Multicast Algorithmus liefert Nachrichten an Prozesse in beliebiger Reihenfolge aus 
- Vielzahl an Ordnungen kann implementiert werden
- ordnen von Nachrichten:
	-  sichert Konsistenz zu, bspw. Kausalität (Ursache vor Wirkung ausliefern)
	- erhöht aber Latenz
- Ordnungen:
	- FIFO-Ordnung: wenn korrekter Prozess multicast(g,m) ausführt und dann multicast(g,m'), dann wird jeder korrekte Prozess, der m' ausliefert, m vor m' ausliefern
	- Kausale Ordnung: wenn multicast(g,m) --> multicast(g,m') gilt (happend before [[Relation]]), dann wird jeder korrekte Prozess der m' ausliefert, m vor m' ausliefern
	- Totale Ordnung: wenn korrekter Prozess m vor m' ausliefert, dann wird jeder andere korrekte Prozess, der m' liefert ebenfalls m vor m' ausliefern
![[Multicast Ordnungen.png]]
- diese Definitionen beinhalten keine Zuverlässigkeit
	- aber geordneter Multicast kann statt B-multicast auch R-multicast verwenden
	- Ordnungen der Nachrichten erfolgt nach B-deliver in der Warteschlange
- totalgeordnete Multicast Auslieferung benötigt zusätzliche Bandbreite und erhöht Latenz
	- deshalb werden wenn möglich effizienteren Ordnungen (z.B.. FIFO oder kausal) für Anwendungen ausgewählt
##### Bsp.: Anzeige aus einem Bulletin-Board Programm
- Nutzer führen Bulletin-Board Anwendungen mit Multicast-Nachrichten aus 
- eine Multicastgruppe pro Thema (z.B. os, interesting)
- erfordert zuverlässigen Multicast- sodass alle Mitglieder die Nachrichten erhalten
![[Bsp. BulletinBoard Beispiel.png]]
### Implementierung der FIFO Ordnung über Basis-Multicast
- FIFO geordneten Multicast mit Operationen FO-Multicast und FO-deliver für nicht-überlappende Gruppen. Er kann über jedem grundlegenden Multicast implementiert werden
- jeder Prozess p verwaltet:
	- $S^p_g$ - Zähler für Nachrichten die von p an g gesendet werden
	- $R^q_g$ - Sequenznummer der letzten Nachricht an g die p von q ausgeliefert hat
- Damit p eine Nachricht an g FO-multicasted, muss der $S^p_g$ an die Nachricht anhängen, diese B-multicasten und $S^p_g$ um 1 erhöhen
- Bei Erhalt der Nachricht von q mit der Sequenznummer S, überprüft p ob S = $R^q_g$ + 1 
	- Falls ja: FO-deliver
	- Falls S > $R^q_g$ + 1: p in Warteschlange, bis ausstehende Nachrichten zugestellt wurden
### Implementierung des total geordneten Multicasts
##### genereller Ansatz
- verwende total geordnete Kennungen(__id__) für Multicast-Nachrichten
- jeder empfangende Prozess trifft Entscheidungen über die Reihenfolge aufgrund der Ids
- ähnelt FIFO: aber Prozesse verwenden gruppenspezifische Sequenznummern
- Operationen: __TO-multicast__ und __TO-deliver__
##### 2 Ansätze für total geordneter Multicast über Basis-Multicast
- Verwendung eines Sequencer-Prozess (für nicht überlappende Gruppen)
- Prozessen einer Gruppe einigen sich gemeinsam auf eine Sequenznummer für jede Nachricht
##### Sequencer
![[Multicast Sequencer Algorithmus.png]]
da die Sequenznummern von einem Sequencer definiert werden, gibt es eine totale Ordnung
wie B-Multicast: Wenn Sender nicht crasht erhalten alle Mitglieder Nachricht
Sequencer kann zum Flaschenhals werden
Sequencer = kritischer Ausfallpunkt:
- kann verbessert werden, indem Nachrichten in f + 1 Knoten gespeichert werden bevor sie gesendet werden.--> es können so bis zu f ausfälle toleriert werden
- Mitglieder informieren ihn über die zuletzt erhaltene Sequenznummer
### Der ISIS Algorithmus für totale Ordnung
![[Multicast ISIS Algorithmus.png]]
Einigung über Sequenznummern:
- jeder Prozess q verwaltet:
	- $A^q_g$ die größte Abgestimmte Sequenznummer, die er gesehen hat
	- $P^q_g$ seine selbst vorgeschlagene größte Sequenznummer
1. Prozess p B-multicasted (m,i) zu g; i ist eindeutige id für m
2. jeder Prozess q antwortet Sender p mit Vorschlag für Nachrichtensequenznummer mit $P^q_g := max(A^q_g, P^q_g) + 1$; verknüpft vorgeschlagene Sequenznummer mit der Nachricht und fügt diese in seine Warteschlange ein
3. P sammelt alle Vorschläge und wählt die größte aus --> "a"; Er B-multicasted (i,a) zu g. Empfänger setzen $A^q_g = max(A^q_g, a)$, fügen a an die Nachricht an und ordnen Warteschlange neu
Warteschlange:
- geordnet: Nachricht mit klneinster Sequenznummer vorne
- wenn abgestimmte Nummer einer Nachricht hinzugefügt wird, wird Schlange neu geordnet
- wenn vorderste Nachricht abgestimmte Id hat, wird sie in Auslieferungsschlange übertragen (auch wenn bereits abgestimmt: nicht vorne in Schlange = nicht übermitteln)
- jeder Prozess stimmt gleiche Ordnung ab und liefert Nachrichten in dieser Reihenfolge --> totale Ordnung
Latenz:
- 3 Nachrichten werden nacheinander gesendet, somit ist Latenz __höher als bei der Sequencer-Methode__
- Diese Ordnung ist ggf. nicht kausal oder FIFO
## Kausal geordneter Multicast
- Algorithmus von Birman 1991 für kausal geordneten Multicast in nicht-überlappenden, geschlossenen Gruppen
- Nutzung der __happend-before__ [[Relation]] (nur für Multicast-Nachrichten) --> Ordnung durch 1-1 Nachrichten bleibt unbeachtet
- Nutzung von __Vektor-Uhr Zeitstempeln__ --> erlaubt Bestimmung der kausalen Vergangenheit von Nachrichten ([[Zeit und globaler Zustand]])
Vektor-Zeitstempel:
![[Multicast Vektor Zeitstempel.png]]
$p_j$ liefert Nachricht aus --> Prozess $p_i$ aktualisiert Vektor Zeitstempel
	Erhöhung des j-ten Elements seines Zeitstempels um 1
Vgl. Vektoruhrenregel: $V_i(j) := max(V_i(j), t(j))$ for j = 1, 2, ..., N
	 in diesem Algorithmus ist klar, dass sich nur das j-te Element erhöht
wenn R-multicast statt B-multicast nutzen ist Protokoll zuverlässig + kausal geordnet
verbinden mit Sequencer Algorithmus --> erhalten kausale und totale Ordnung
# Zusammenfassung
- Multicast Kommunikation kann Anforderungen an Zuverlässigkeit und Reihenfolge durch Integrität, Validität und Einigung spezifizieren
B-multicast:
- ein korrekter Prozess wird die Nachricht übermitteln, wenn der Multicaster nicht crasht
zuverlässiger Multicast:
- korrekte Prozesse einigen sich auf Menge auszuliefernder Nachrichten
- 2 Implementierungen vorgestellt: über B-multicast und IP-multicast
Auslieferungsreihenfolge:
- FIFO, totale und kausale Lieferordnung
- FIFO Ordnung durch Sender Sequenznummern
- totale Ordnung durch Sequencer oder Einigung über Sequenznummer zwischen Prozessen einer Gruppe
- kausale Ordnung durch Vektor-Zeitstempel
Warteschlange ist nützlich Komponente für Implementierung von Multicast-Protokollen