---
tags: Uni Syskon
---
# nebenläufiges Programm
- einfache Sicht: gleichzeitige Ausführung mehrerer miteinander **verschachtelter** Befehle, jeweils aus verschiedenen Prozessen/[[Threads]]
- beschreibt gleichzeitige Ausführung mehrerer interagierender Prozesse auf einem oder mehrerer Prozessoren
### Definition 2.2
Ein nebenläufiges Programm besteht aus einer endlichen Menge interagierender Prozesse $Π = {p (1) , …, p (l)}$, die auf einer Menge von Ressourcen $R_Π$ ausführen. Hierbei gilt: 
1. Die Ausführung kann durch eine Sequenz von atomaren Befehlen beschrieben werden, in der jeweils genau ein Prozess voranschreitet. 
2. Paare von Prozessen können sich Ressourcen aus $R_Π$ teilen und deren Belegung durch Ausführung eines Befehls jeweils ändern. 
3. Nach Ausführung eines atomaren Befehls auf einer gemeinsamen Ressource $r ∈ R_Π$ sind Veränderungen der Belegung von $r$ im nächsten Ausführungsschritt sichtbar

### Eigenschaften verschachtelter Programme
- Korrektheit
- Zustand und Invarianten des Zustands von großer Bedeutung
- müssen mehrere Verschachtelungen erwarten und kontrollieren (Synchronisierung) --> falsche Verschachtelungen ausschließen
- eine Abstraktion sollte unabhängig sein von der realen Zeit/Dauer, in der einzelne Befehle ablaufen
	--> verwenden von Zeitannahmen problematisch:
	- Ausführungsdauer abhängig von Rechenlast
	- Ausführungszeitpunkt nicht vorhersehbar
	- Ausführungsgeschwindigkeiten variieren (große Systemabhängigkeit)

### Modellierung von [[Nebenläufigkeit]]
- betrachte nur Zustandsübergänge
- Zustandsänderung nach atomaren Schritt
- unterscheide zwischen Programm und Prozess
	- Programm definiert Befehle
	- Prozess ist das Programm in der Ausführung

## Prozess
- ein Prozess beschreibt den Ausführungszustand eines Programms
- ein Prozess beinhaltet
	- **Programmtext**: atomare Operationen (Load, Push,...)
	- **Ausführungskontext**: Programmzähler, Prozessor (Akkumulator, Adressregister, Prozessorstatus,...)
	- **Daten**: Variablen, Zustand Prozeduraufrufe
- Prozesse benötigen **Ressourcen** zur Ausführung: CPU, Speicher, Geräte
- Kontroll- und Zustandsinformationen ermöglichen Sicherung des Ausführungszustands eines Programms
- Uniprozessorsystem: Zustandssicherung ermöglicht **quasi-parallelen** Ablauf mehrerer Prozesse
- Mehrprozessorsystem: **Migration** zwischen Prozessen möglich
### Definition 2.1
Ein Prozess p besteht aus einem Tupel (P, Z), mit 
1. P = {p1 , p2 , … , pn }, eine Zerlegung des Programmtextes in atomare Befehle 
2. Z = {z1 , z2 ,…, zm}, die Menge von Kontroll- und Zustandsinformationen
Insbesondere definiert cp = pi den in einer Ausführung als nächstes ausführbaren Befehl.
![[Abstrakte Sicht auf einen Prozess.png]]

### Interaktion
#### Interaktion über gemeinsame Ressourcen
- mehrere Prozesse können sich Ressourcen teilen
	- ermöglicht Interaktion zwischen Prozessen (z.B. über gemeinsamen Speicherbereich --> **Shared Memory Segment**)
	- Zustand gemeinsamer Ressourcen definiert Reigenfolge ihres Zugriffs
	- Uniprozessorsystem: nur eine atomare Operation
	- Mehrprozessorsystem: Speicher stellt Atomizität der parallelen Operationen sicher
#### Interaktion über Kommunikation
- Zustandsänderung aufgrund des Austauschs von Nachrichten ermöglicht Interaktion von Prozessen auf unterschiedlichen Systemen und Systemen ohne gemeinsamen physischen Speicher
- Kommunikation über send(Empfänger, Wert) und receive(Wert) Operationen

## Zustand einer nebenläufigen Ausführung
- Zustand nebenläufiges Programm: Menge der Kontroll- und Zustandsinformationen sämtlicher beteiligter Prozesse
### Zustandsübergänge
- jeder atomar ausgeführte Befehl eines nebenläufigen Programms beschreibt einen Zustandsübergang
- Bsp.: ![[Zustandsübergangsbeispeil.png]]

### Implikationen
#### Verschachtelung
- Bsp.: $p = {p1, p2} und q = {q1, q2}$ --> insgesamt 6 mögliche Verschachtelungen
- Beachte: **sequentielle Anordnung** der Prozesse bleibt! (siehe [[Nebenläufigkeit]])
#### Semantik
- Die Ausführungssequenz beeinflusst die Semantik --> je nachdem welche Verschachtelung stattfindet, können unterschiedliche Ergebnisse Entstehen

#### Szenario
- ein Szenario wird durch eine **Folge von Zuständen** definiert

#### Anwendbarkeit der Abstraktion
- beachte Unterschiede:
	- Modell: sequentielle Ausführung verschachtelter Befehle und globale Sicht auf den Systemzustand
	- Systeme: parallel ablaufende Ausführungsschritte und keine globale Sicht
- trotzdem ist die Modellierung nebenläufiger Programme sinnvoll

## nebenläufiges Programm auf Multitaskingsystem
- Multitaskingsystem: Software, die den Ablauf mehrerer Prozesse auf einer CPU unterstützt
- [[Unterbrechungsbehandlung]](UBR) auf Hardwareebene ermöglicht Systemsoftware Kontrolle über die Ressourcen (periodisch oder durch Ereignis)
- nach UBR privilegierte Befehle:
	- Steuerung von Geräten
	- Zuweisung von Ressourcen an Prozesse
	- Fortsetzung eines anderen Prozess (Prozesswechsel)
### Prozesswechsel
- Systemsicht: Kontextwechsel zwischen [[Betriebssystem]](BS) und Prozessen
erfordert:
1. System sichert den Zustand des aktiven Prozess
2. System wählt nächsten Prozess aus ($P_next$)
3. Weist $P_next$ die benötigten Ressourcen zu
4. Übergibt Kontrolle an $P_next$

## nebenläufiges Programm auf Uniprozessor
- Wechsel zwischen BS und [[Betriebssystem]] ermöglicht beliebige Verschachtelungen --> entspricht Modellierung nebenläufiger Programme
- Bsp.: ![[Systemsicht vs. Programmsicht.png]]

## nebenläufiges Programm auf Multiprozessor
- Prozesse können auf verschiedenen Prozessoren ausführen
- unterscheide:
	- lokale Ressourcen: **Cache** und **lokaler Speicher** --> effiziente Ausführung eines Prozess
	- gemeinsame Ressourcen: **gemeinsamer Speicher** --> Aktualisierung des gemeinsamen Speichers
### Crossbarswitch
- ermöglicht atomaren Zugriff auf gemeinsamen Speicher in symmetrischen Rechnerarchitekturen (symmetrisches Multiprozessorsystem SMP)
- ![[Crossbarswitch.png]]
### Ablauf der Prozesse auf mehreren Prozessoren
- Extremfall: alle Prozesse gleichzeitig, maximal ein Prozess pro Prozessor
- Zwei Fälle für eine Ausführung
	1. atomare Befehle auf lokalen Ressourcen: Betrachten der Zustandsübergänge einer beliebigen Verschachtelung reicht.
		Bsp.:![[Verschachtelung bei Zugriff auf lokalen Speicher.png]]
	2. atomare Befehle auf gemeinsame Ressourcen: Zustandsübergänge bestimmt durch Veränderung der Belegung von lokalen und gemeinsamen Ressourcen.
		Bsp.: p1 --> q1: n = 1 ABER q1 --> p1: n = 2
### Satz 2.1
In einem Multiprozessorsystem führen je zwei Sequenzen von Zustandsübergängen in einem nebenläufigen Programm zum selben Endzustand, wenn sie folgende Eigenschaften erfüllen: 
1. Die sequentielle Ordnung der Befehle eines Prozesses bleibt erhalten 
2. Die Ausführungsordnung von Befehlen auf atomar veränderbaren gemeinsamen Ressourcen bleibt erhalten

## nebenläufiges Programm in verteilten Systemen
### Satz 2.2
In einem Verteilten System führen je zwei Sequenzen von Zustandsübergängen in einem nebenläufigen Programm zum selben Endzustand, wenn sie folgende Eigenschaften erfüllen: 
1. Die sequentielle Ordnung der atomaren Befehle eines Prozesses bleibt erhalten 
2. Die Ausführungsordnung von Befehlen unter Einhaltung der Sende/Empfangs-[[Relation]] bleibt erhalten
--> genau wie bei Multiprozessorsystemen, keine Annahmen über Zeit notwendig
##### Beispiel verteilte Ausführung
![[verteilte Ausführung.png]]
