---
tags: Uni Syskon
---
# Replikation
## Einführung
[[Middleware]] ermöglicht einfache Servicenutzung; Populär und einfach: objektorientierte [[Middleware]]
ABER: wenn n Objekte für Ausführung kritisch sind, wie können Zuverlässigkeit und Fehlerstabilität garantiert werden?
--> Replikation ist eine Idee, aber sieht es dann noch nach einem Objekt aus? --> Replikationstransparenz
--> 100 fehlerhafte Server bleiben fehlerhaft --> Fehlertransparenz und angemessene Konzepte notwendig
--> Wie System kontrollieren und konfigurieren - während es arbeitet --> Bestimmung sicherer Zustände (globale konsistente Schnitte/Beendigungen)
### Fehlermodell (F. Schneider)
##### Crash
Server stoppt verfrüht. Bis dato arbeitete er korrekt, erholt sich nie mehr (fail-stop)
##### Crash-link
Server kann crashen oder Verbindung kann Nachrichten verlieren (aber keine verzögerten, korrupten, doppel-Nachrichten)
##### Empfangsversäumnis
Server kann abstürzen, aber auch Nachrichten nicht empfangen, die von einer korrekten Verbindung direkt an ihn adressiert sind
##### Sendeunterlassung
Server kann Abstürzen oder das Senden von Nachrichten über eine korrekte Verbindung auslassen
##### Allg. Auslassung
Auslassung beim Senden/Empfangen
##### Beliebig (einschließlich byzantinisch)
kann auch vorsätzliches Verhalten (Angriffe) zeigen
### Redundanz hilft
n Server --> f < n fehlerhafte Server kann man tolerieren
n Server --< Mehrheitsentscheidungen möglich (beachte Quorum) und n/2 - 1 fehlerhafte Server isolieren
wissen von bösartigen Servern, die zusammenarbeiten, und Sie wollen Einigung erzielen --> benötigen Mehrheit von n > 3f + 1 fehlerhaften Servern
### Voraussetzung
Protokolle zur Aktualisierung und zum Zugriff auf Replikate erforderlich
Die Integration in [[Middleware]] kann Tatsache verschleiern, dass ein Objekt repliziert wird, d.h. mehrere physische Kopien existieren
## Grundlagen der Replikation
- es gibt mehrere physische Kopien einzelner Daten (oder Server)
- jede Kopie wird Replikat genannt
- jeder Prozess, der mit den Daten arbeitet kann auf jede dieser Replikate zugreifen wenn alles korrekt abläuft beinhaltet jedes Replikat der Daten die gleichen Informationen
### warum Replikation?
__Performance-Verbesserung__
- [[verteilte Systeme]] müssen in ihrer Größe und geographischen Ausdehnung erweiterbar sein
- mehrere Server mit replizierten Daten geben unterschiedlichen Prozessen darauf Zugriff
- Zugriffszeit abhängig vom verwendeten Server --> Speedup möglich
__Fehlertoleranz-Service__
- garantiert korrektes Verhalten trotz Fehlern
- wenn f von f + 1 Servern crashen gibt es noch einen der den Dienst anbietet
- wenn f von 3f + 1 Servern byzantinische Fehler haben kann das Gesamtsystem einen korrekten Dienst anbieten
__Verfügbarkeit__
- wird beeinträchtigt:
- Serverausfälle: Repliziere Daten auf Ausfall-unabhängige Server; wenn ein Server ausfällt kann Client einen anderen Verwenden
- Netzwerkpartitionen und getrennter Betrieb: Nutzer mobiler Computer unterbrechen die Verbindung freiwillig und lösen Konflikte der Datenerhaltung bei der Neuverbindung auf; erfordert Abstimmung über Daten (Quoren, Integrationsprotokolle)
### Anforderungen an replizierte Daten
##### Replikationstransparenz
Clients können logische Objekte sehen (nicht mehrere physische Kopien)
Sie greifen auf ein logisches Objekt zu und erhalten ein Resultat
##### Konsistenz
Alle Replikate sollten "den gleichen" Zustand haben:
- wenn z.B. ein Benutzer eines Kalenders die Verbindung unterbricht, kann die lokale Kopie mit den anderen nicht Konsistent sein und muss bei einer erneuten Verbindung abgeglichen werden. 
- verbundene Clients mit unterschiedlichen Kopien sollten das gleiche Resultat erhalten diese Probleme werden in verteilten Datenbanken behandelt
## Systemmodell
- jedes logische Objekt ist durch eine Menge an physischen Kopien, genannt Replikate, implementiert die Replikate sind nicht notwendigerweise immer konsistent
- einige können Updates erhalten haben, die noch nicht auf die anderen übertragen wurden
Annahmen:
- synchrones System (Nachrichten haben bekannte obere Schranke der Verzögerung)
- Prozesse sind nur fehlerhaft wenn sie crashen
- keine Netztwerkpartitionen
Replikationsmanager (RM)
- RM verwaltet Replikate auf einem Knoten und adressiert sie direkt
- RMs führen wieder herstellbare Operationen auf den Replikaten aus. Sie hinterlassen keine inkonsistenten Resultate wenn sie crashen
- Objekte werden bei allen RMs kopiert, wenn nicht anders festgelegt
- statische Systeme basieren auf einer fixen Anzahl von RMs
- Dynamische Systeme: RMs können kommen und gehen (z.B. wenn sie crashen, Wiederstart möglich)
- Ein RM ist als Zustandsmaschine (starte machine) mit den folgenden Eigenschaften realisiert:
	- Operationen werden atomar durchgeführt
		- Operationen sind geordnet (z.B. kausal, total)
		- Reigenfolge der Operationen ist bei jedem Replikat identisch
	- Der Zustand ist eine deterministische Funktion des internen Zustands sowie der ausgeführten Operationen
		- alle Replikate starten identisch und führen die gleichen Operationen aus
	- Die Operationen dürfen nicht durch das externe Effekte, bspw. Zustand der Uhren, Rechnerlast, etc. beeinflusst werden
## grundlegendes architektonisches Modell zum Management replizierter Daten
- Menge von RMs bietet Dienste für Klienten an
- Klienten sehen einen Dienst, der ihnen Zugriff auf ein logisches Objekt gibt, das transparent für sie auf den RMs repliziert ist 
- Clients stellen Anfragen an den RM:
	- lese Operationen (read-only request)
	- Aktualisierungsoperationen (update-requests)
- Client-Anfragen werden durch Front End verwaltet und umgesetzt --> ein Front End (FE) macht die Replikation transparent
## Anfrage eines Objekts: 5 Phasen
##### 1. Stellen der Anfrage an das FE
Das FE:
- sendet die Anfrage entweder zu einem einzelnen RM, das sie ggf. an andere RM weiterleitet
- oder stellt die Anfrage an alle RMs
##### 2. Koordination
- die RMs entscheiden , ob sie die Anfrage ausführen
- Anfrage wird in Reihe anderer Anfragen eingeordnet/verschränkt
- FIFO, kausale Reihenfolge, totale Reihenfolge
##### 3. Ausführung
- RMs führen die Anfrage aus 
##### 4. Einigung
- RMs erzielen Einigung (Konsens) über die Auswirkungen der Anfrage
##### 5. Antwort
- ein/mehrere RMs antworten dem FE, z.B.
	- für hohe Verfügbarkeit wird erste Antwort gesendet
	- um weitere Fehler zu korrigieren: Abstimmung
beachte: Reihenfolge der Phasen und ihrer Inhalte sind systemabhängig
## Gruppenkommunikation - Prozessgruppen
- Prozessgruppen sind nützlich, um replizierte Daten zu verwalten
Gruppenzugehörigkeitsdienste beinhalten:
- Interface um Mitglieder hinzuzufügen/zu entfernen
	- Erstellung/Löschen von Prozessgruppen
	- Hinzufügen/Entfernen von Mitgliedern
	- ein Prozess kann generell mehreren Gruppen zugeordnet sein
- Fehlerdetektor (stellt synchrones System her)
	- überwacht Mitglieder auf Fehler (Crashs/Kommunikation)
	- Ausschluss bei Nichterreichbarkeit/Timeout
- informiert Mitglieder über Änderungen der Mitgliedschaft
- Ausweitung von Gruppenadressen
	- Multicasts an Gruppenidentifikatoren adressiert
	- Bereitstellung von Koordinaten, wenn sich Mitgliedschaft ändert
### Dienste für Prozessgruppen
![[Dienste für Prozessgruppen.png]]
#### Fehlertoleranzdienste
Bereitstellung eines korrekten Dienstes, selbst wenn f Prozesse fehlschlagen 
- durch Replikation von Daten und Funktionalitäten bei den TMs
- intuitiv ist ein Prozess korrekt, wenn er trotz Fehlern antwortet und Clients nicht zwischen replizierten Daten und einfachen Kopie unterscheiden können
- es muss jedoch sichergestellt werden, dass eine Menge von Replikaten die gleichen Resultate wie eine einzige Kopie ergeben
Annahmen:
- verlässliche Kommunikation
- keine Partitionen
- RMs verhalten sich entsprechend der Spezifikationen/eines Crashs
#### Beispiel: ein naives Replikationssystem
- RMs an den Maschinen A und B behalten Kopien von x und y
- Clients benutzen lokalen RM wenn verfügbar, sonst den anderen
- RMs propagieren gegenseitig Updates, nachdem sie dem Client geantwortet haben
Client 1: setBalanceB(x,1); setBalanceA(y,2)
Client 2: getBalanceA(y)->2; getBalanceA(x)->0
1. Ausgangskontostand von x und y ist 0 Euro
2. Client 1 updated X bei B (lokal) und merkt dann, dass dabei ein Fehler auftrat, deshalb benutzt er A
3. Client 2 liest den Kontostand bei A (lokal) da Client 1 y nach x updated, Client 2 sollte 1 Euro für x sehen
Beobachtung: das ist nicht das Verhalten, das auftreten würde, wenn A und B auf dem gleichen Server implementiert wären
Systeme zur Replikation von Objekten können unter Ausschluss dieses unnormalen Verhaltens konstruiert werden
Wir werden nun diskutieren, was unter korrektem Verhalten in einem Replikationssystem verstanden wird
## korrektes Verhalten in einem Replikationssystem
### Linearisierbarkeit - das strengste Kriterium für ein Replikationssystem
- ein Dienst für replizierte Objekte ist linearisierbar, wenn es für jede Ausführung eine Verschränkung von Client-Operationen gibt, sodas:
	- die verschränkte Operationssequenzen die Spezifikationen einer (einfachen) korrekten Kopie erfüllen
	- die Reihenfolge der Operationen in der Verschränkung konsistent mit dem Zeitpunkt ist, zu der sie tatsächlich stattgefunden haben
- für jede Menge von Client Operationen gibt es eine Verschränkung (die für eine Menge einzelner Objekte korrekt wäre)
- Jeder Client hat eine Sicht auf die Objekte die konsistent ist, d.h. die Resultate der Client-Operationen machen Sinn innerhalb der Verschränkung
Beobachtung: das Bankenspiel hat keinen Sinn gemacht --> wenn das zweite Update ausgeführt wird, sollte das erste auch ausgeführt werden
ABER: Linearisierbarkeit sollte nicht in transaktionalen Replikationssystemen verwendet werden
Die Echtzeit-Anforderungen ist durch Zeitschranken bei der Verarbeitung schwer durchzusetzten
- Uhren können nur innerhalb von Schranken synchronisiert werden 
- Verarbeitung kostet Zeit und Umordnung kann Echtzeitkriterium brechen
### sequentielle Konsistenz
- ein replizierter, geteilter Dienst ist sequentiell konsistent, wenn es für jede beliebige Ausführung eine Verschränkung von Client-Operationen gibt, sodass:
	- die Verschränkungssequenz der Operationen die Spezifikationen einer (einfachen) korrekten Kopie des Objekts erfüllt
	- die Reihenfolge der Operationen in der Verschränkung konsistent mit der Programmreihenfolge ist, mit der jeder Client sie ausführte
### Bsp.: Linearalisierung vs. sequentielle Konsistenz
Client 1: setBalanceB(x,1);
Client 2: getBalanceA(y)->0; getBalanceA(x)->0
Client 1: setBalanceA(y,2);
- das Beispiel ist sequentiell konsistent aber nicht linearisierbar
- dies ist möglich, da unter einer naiven Replikationsstrategie, selbst wenn weder A noch B fehlerhaft sind B's Update noch nicht zu A propagiert wurde wenn Client 2 es liest
- es ist nicht linearisierbar, da in Wahrheit Client 2's Update getBalance nach Client 1's Update setBalance stattfindet
- ABER: folgende Verschachtelung erfüllt beide Kriterien für sequentielle Konsistenz: getBalanceA(y)->0; getBalanceA(x)->0; setBalanceB(x,1); setBalanceA(y,2)
### das passive (primary-Backup) Modell für Fehlertoleranz
- zu jeder Zeit gibt es einen primary RM und mehrere secondary (backup, slave) RMs
- FEs kommunizieren mit dem primary RM
	- Primary RM führt Operation aus und sendet Kopien der upgedateten Daten des Results an die backup RMs
- wenn der primary RM ausfällt, agiert einer der backup RMs als neuer primary RM
![[primary Backup Modell Replikation.png]]
#### passive Replikation Überblick
- nicht deterministisches Verhalten möglich, z.B. Multithread-Operationen
- n RMs sind fehlertolerant zu n-1 Prozess-Crashs
- keine Toleranz gegenüber einzelnen fehlerhaften Replikaten oder byzantinischen Fehlern (zufällige und koordinierte Fehler)
- Verzögerung wenn primary RM ausfällt, da neuere primary RM eingesetzt werden muss
#### passive Replikation: Anfrageprozess in 5 Phasen
##### 1. Anfrage
FE stellt Anfrage mit eindeutiger Identifizierung an den primary RM
##### 2. Koordination
Primary RM nimmt Anfragen in FIFO Reigenfolge an. Wenn die Anfrage bereits ausgeführt wurde erfolgt erneute Zusendung der Antwort
##### 3. Ausführung
Primary RM führt Anfrage aus und speichert die Antwort
##### 4. Einigung
wenn Anfrage ein Update ist, sendet der primary RM einen Identifier zu allen backup RMs
##### 5. Antwort
Primary RM antwortet dem FE
wenn der primary RM ausfällt, agiert einer der backup RMs als neuer primary RM (benötigt eine Wahl)
### aktive Replikation für Fehlertoleranz
- RMs sind Zustandsmaschinen, die alle die gleiche Rolle spielen und als Gruppe organisiert sind
	-  alle starten im gleichem Zustand und führen die gleichen Operationen aus, sodass ihr Zustand identisch bleibt
	- Notwendig: zu Grunde liegender [[Multicast]] ist (total) geordnet und zuverlässig
- Wenn ein RM crasht hat das keine Auswirkung auf die Performance des Diensts, da die anderen normal weiterarbeiten
- Fehler bei Dienstausführung können maskiert werden, da das FE die Antworten, die es erhält sammeln und vergleichen kann (Vorsicht: das gilt nur bei zugrundeliegendem [[Multicast]])
#### aktive Replikation: Anfrageprozess in 5 Phasen
##### Anfrage
FE multicastet Anfrage mit eindeutigem Bezeichner zu einer Gruppe von RMs
##### Koordination
das Kommunikationssystem liefert die Anfrage an jeden korrekten RM in der gleichen (totalen, kausalen, etc.) Reihenfolge
##### Ausführung
Jeder RM führt die Anfrage aus - korrekte RMs führen die Anfrage identisch aus
##### Einigung
keine Einigung nötig, da der [[multicast]] die entsprechende Semantik bereitstellt
##### Antwort
Jeder RM sendet seine Antwort an das FE. Die Anzahl der Antworten, die das FE sammelt hängt von der Fehlerannahme und vom [[Multicast]]-Algorithmus ab
#### aktive Replikation Überblick
- n RMs sind fehlertolerant zu n-1 Prozess-Crashs (keine byzantinische Fehlertoleranz)
- n RMs sind fehlertolerant zu n/2 - 1 Verarbeitungsfehlern wenn das zugrundeliegende Multicastsystem entsprechende Zustellgarantien bietet
- Mehr Overhead - jede Anfrage muss von jedem RM bearbeitet werden
- keine Verzögerung oder Crashs - jeder RM ist up to date
- Beachte: beliebige Fehler benötigen 3f + 1 korrekte Replikate, um f fehlerhafte zu tolerieren
## zum Fehlermodell (F. Schneider)
Was sind beliebige Fehler?
Bislang: Knoten: totaler Ausfall (crash, fail-stop), Kommunikation: Übertragungsfehler
noch nicht bekannt: 
- (Ver-)fälschen von Nachrichten (Inhalt, Absender, Empfänger)
- beliebige Verzögerung von Nachrichten (asynchrones System)
- Fehler in Dienstausführung: Crash/Wiederstart, sporadisch
- Angriffe: gezielte Verfahren, auch abgestimmt zwischen Knoten
### Byzantinische Generäle
- n Prozesse kommunizieren über Nachrichten
- jeder Prozess kann direkt mit jedem anderen sprechen
- synchrones System, keine Fälschung der Nachrichten bzw. Absender oder Auslassung (Lamport: mündliche Nachricht)
- ein ausgezeichneter Prozess (Commander) initiiert die Abstimmung und teilt den anderen Prozessen (Lieutenant) seine Entscheidung mit korrekter Lösung, wenn:
	- IC1: alle korrekten Prozesse befolgen dieselbe Nachricht
	- IC2: wenn der Initiator korrekt ist, wird jeder korrekte Prozess dessen Entscheidung folgen
#### Problem mit 3 Prozessen
zwei korrekte Prozesse können bei einem fehlerhaften Prozess kein korrektes Ergebnis garantieren (rot = fehlerhaft)
![[Byzantinische Generäle mit 3 Prozessen.png]]
##### Satz
Das byzantinische Generäle Problem ist bei m fehlerhaften Prozessen nur lösbar für n >= 3m + 1 (ohne Beweis)
#### Problem mit 3 korrekten und 1 fehlerhaften Prozessen
##### Lieutenant fehlerhaft
![[Byzantinische Generäle Problem Lieutenant fehlerhaft.png]]
##### Commander fehlerhaft
![[Byzantinische Generäle Problem Commander fehlerhaft.png]]
#### Algorithmus (Lamport/Shostak/Pease)
rekursiver Algorithmus, löst BG für n >= 3m + 1 Prozesse mit maximal m fehlerhaften Prozessen
"oral message": keine Verluste, Verfälschungen, Auslassung von Nachrichten
Es existieren eine Mehrheits-Funktion auf den ausgetauschten Werten
OM(0)
1. Der Initiator (Commander) schickt seinen Wert an jeden anderen Prozess (Lieutenant)
2. jeder andere Prozess übernimmt den Wert des Initiators oder $\perp$ falls er keinen Wert erhält
OM(m), m>0
1. Der Initiator schickt seinen Wert an jeden anderen Prozess
2. Für alle i aus {1,...,n}:sei $v_i$ der Wert, den Prozess $p_i$ vom Initiator empfangen hat oder $\perp$ falls er keinen Wert erhält. Jeder Prozess $p_i$ führt O(m - 1) als Initiator aus und sendet $v_i$ an die verbleibenden n - 2 Prozesse
3. Für alle i aus {1,...,n} und i $!=$ j sei $v_j$ der Wert, den Prozess $p_i$ von Prozess $p_j$
4. erhält (aus O(m - 1) aus Schritt 2) oder $\perp$. $p_i$ verwendet Mehrheit ($v_1,...,v_{n-1})
##### Nachrichtenaufwand
1. Runde: 1 Instanz mit n-1 Nachrichten
2. Runde: n-1 Instanzen mit je n-2 Nachrichten
3. Runde: (n-1)(n-2) Instanzen mit je n-3 Nachrichten
(m + 1)Runde: (n-1)!/(n-1-m)! Instanzen mit je n-1-m Nachrichten
--> O($n^{m+1}) Nachrichten
#### verwandte Probleme
##### Byzantinische Generäle
- ein Wert wird von einem ausgezeichneten Prozess vorgegeben
- alle korrekten Prozesse einigen sich auf den gleichen Wert (IC1)
- ist der vorgebende Prozess fehlerfrei, erfolgt die Einigung auf dessen Wert (IC2)
##### interaktive Konsistenz
- von jedem Prozess wird ein Wert vorgegeben
- alle korrekten Prozesse einigen sich auf den gleichen Wertevektor
- die Vorgabewerte korrekter Prozesse werden in dem Wertevektor richtig wiedergegeben
##### Konsenz
- von jedem Prozess wird ein Wert vorgegeben
- alle korrekten Prozesse einigen sich auf den gleichen Wert
- wenn alle korrekten Prozesse den gleichen Wert vorgeben, einigen sich alle auf diesen Wert
### Fehler/Koordination in [[verteilte Systeme]]n in synchronen Systemen lösbar
- Überführung asynchrone Systeme benötigt Fehlerdetektoren
- einfache Fehler lassen sich durch aktive/passive Replikation maskieren
- Mehrheitsentscheid möglich - benötigt aber [[Multicast]]mechanismen 
- byzantinische Fehler erfordern aufwändigere Algorithmen mit höherem Kommunikationsaufwand und Anzahl korrekter Knoten (n >= 3m + 1)