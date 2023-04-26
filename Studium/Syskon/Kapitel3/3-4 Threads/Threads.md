---
tags: Uni Syskon
---
# Threads
## wichtigste Konzepte hinter Prozessen
beide folgende Aspekte können entkoppelt werden: nebenläufige Ausführungsstränge(Threads) teilen sich gemeinsame Prozessressourcen
### Besitz von Ressourcen
- virtueller Adressraum ist einem Prozessabbild zugeordnet (Programm, Speicher(Daten, Heap, Stapel))
- E/A: offene Dateien, Netzwerkverbindungen, usw.
- [[Betriebssystem]] bietet Schutzmechanismen für die Ressourcen (Isolation zwischen Prozessen)
### [[Scheduling]]
- Verzahnung der nebenläufigen [[Programmausführung]]
- Ausführungszustand (bereit, aktiv, etc.)

## Vergleich: Prozesse und Threads
**Multithreading**
- mehrere Ausführungsstränge (Threads) pro Prozess
- Threads können in der gleichen Prozessumgebung ausgeführt werden und auf gemeinsamen Prozessressourcen kooperieren
- Verwaltungseinheit für [[Scheduling]] --> Thread
- Verwaltungseinheit für Ressourcen-Management --> Prozess

## lokale Thread-Variablen in Java
```java
public class FooThread extends Thread {
	private static final TheadLocal<Integer> myOwnNumber = new ThreadLocal<Integer>() { //myOwnNumber nicht geteilt mit anderen threads
		//Sets initial value if not explicity set before through set(value)
		@Override protected Integer initialValue() {
			return 0;
		}
	}
	@Override public void run() {
		int x = myOwnNumber.get(); // Returns inital value (0)
		myOwnNumber.set(x+1); // Does not influence variabel value of other threads!
	}
}
```
## Prozess und Thread
- einfache und leichtgewichtige Kommunikation
- Threads teilen sich Speicher und Dateien 
- Kommunikation erfordert nicht den Kern des [[Betriebssystem]]
- Parallelität innerhalb eines Prozesses
- Überlappung von E/A und Berechnungen
- Parallele Ausführung auf einem Multiprozessorsystem
- Reduktion des Zeitaufwands
- Erstellung/Terminierung: Wechsel zwischen Threads innerhalb desselben Prozesses
### Prozess
ein virtueller Adressraum --> Prozessabbild
globale Variablen, Dateien, Kindprozesse, usw.

### Thread
eigener Ausführungszustand und Kontext (Thread Control Block TCB)
eigener Stapel (Thread-lokale Variablen, lokale Funktionsaufrufe)
gemeinsamer Zugriff auf Prozessressourcen, insbesondere Speicher

## Kommunikation
### Interprozesskommunikation
![[Interprozesskommunikation.png]]
Bsp.: Pipes(z.B. Zeilen mit bestimmten String zählen in Textdatei - Ausgabe durch cat, filtern durch grep --> drei Prozesse)

UNIX-Philosophie (Douglas Meltroy): make each program do one thing well, expect the output of every program to become input to another
### Kommunikation über gemeinsame Variablen
Lesen-/Schreiben von gemeinsamen Variablen
- kein Kopieren von Speicher
- keine Kontextwechsel
	- abhängig vom Synchronisationsmechanismus
- erfordert Thread-Synchronisierung
	- nicht trivial

## Implementierung
### auf Benutzerebene
Kern hat kein Wissen über Threads
Thread-Bibliothek verwaltet Ausführung zur Laufzeit
---> Positiv: benutzerdefiniertes [[Scheduling]], lauffähig auf jedem [[Betriebssystem]], leichtgewichtiger (keine Kontextwechsel)
---> Negativ: blockierende Zustände blockieren alle Threads, keine Aufteilung von Threads auf verschiedene Prozessoren
### im Kern
Kern verwaltet Kontext von Prozessen und [[Threads]]
---> Positiv: kein Problem mit Blockieren von einzelnen Threads, Aufteilung von Threads auf (mehrere) Prozessen möglich
--> Negativ: kein benutzerdefiniertes [[Scheduling]], overhead: -kontextwechsel, -Kern involviert für Starten, Umschalten, Terminierung
### Hybride Implementierung
Multiplexing von Threads der Benutzerebene auf Threads im Kern
Idee: Vorteile beider Ansätze kombinieren
![[hybride Implementierung Threads.png]]

## Thread-Zustände
Thread **bereit** oder **aktiv**:
Kernel-Level-Threads
- Kernel kennt Zustand aller Threads
- Kernel (-Scheduler) kann bereite Threads aktivieren
User-Level-Threads
- User-Level-Scheduler kann Threads aktivieren
- Kernel kennt aber nur Prozess, nicht die Threads
- aktive Threads können nur ausführen, wenn Prozess aktiv

Thread __blockiert__:
Kernel-Level-Threads
- blockierter Thread blockiert nicht Ausführung anderer Threads
User-Level-Thread:
- blockierender Systemaufruf eines Threads blockiert gesamten Prozess (alle Threads)

__Suspendierung__ eines Prozesses betrifft alle Threads
__Terminierung__ eines Prozesses betrifft alle Threads

shared Variablen in Java: 
```java
	private static volatile int n = 0;
```
warten mit join (warten bis Thread terminiert): 
```java
	threadname.join();
```
Unterbrechen mit Interrupt: 
```java
t.join(40);
t.interrupt(); //warte nur begrenzte Zeit
```
