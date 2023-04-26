---
tags: Uni Syskon
---
# Semaphore
Lösung __starker Formulierung des KA-Problems__, für __beliebige viele [[Threads]]__ und __kein Busy-Waiting__ von Dijkstra
Annahmen: [[Betriebssystem]] kann faire Spin-Locks mit RMW-Operationen nutzen (Bsp. Ticket-Locks)
--> stellt konsistente nebenläufige Aktualisierung des Semaphors sicher (sonst Henne-Ei-Problem)

gemeinsame Zustandsvariablen durch BS verwaltet, BS stellt atomare Veränderungen sicher, Zugriff über Systemaufrufe: wait(): warte wem mehrere [[Threads]] im KA
signal(): gibt Signal, das Thread KA verlassen hat

Thread __blockiert bei Konflikt__ -->
- kein aktives warten
- BS verwaltet Warteschlange
- Aktivierung, wenn Konflikt nicht mehr existiert

## Datenstruktur eines Semaphors
besteht aus 2 Elementen: 
- integer (binary) value: wie viele [[Threads]] können Semaphor passieren
- queueType queue: Warteschlange von blockierten [[Threads]]
--> Initialisierung: Semaphor S<-(k, leere Menge)

wait(): dekrementieren von value, Thread blockiert in queue wenn value <= 0
signal(): inkrementieren von value

--> mehrere [[Threads]] können Semaphor gleichzeitig passieren, negative Werte für value = Anzahl blockierter [[Threads]] in queue

## KA mit Semaphor
![[KA mit Semaphor.png]]
beachte: wait != await (0% Prozessorauslastung vs. 100%)
erfüllt: wechselseitigen Ausschluss, keine Verklemmung, kein Aushungern --> benötigt __faire Implementierung__ (der Warteschlange): FIFO fair, Heap unfair, Menge Zufall; Aushungern bei nicht fairem [[Scheduling]] möglich

Szenario von vorhin: kein Aushungern: [[Threads]] TN und TH: Fortschritt von TN in KA kann nicht dauerhaft durch TH im Präprotokoll behindert werden: TH wird blockiert --> TN verlässt KA

Szenario: [[Threads]] TN, TM, TH
TM in nicht KA --> TN im KA aber nicht aktiv, da TM aktiv --> TH wartet mit Semaphor auf TN ⚡
--> kann im Kern vom [[Betriebssystem]] aufgelöst werden: __Prioritätenvererbung__
TN erbt Temporär (hohe) Priorität von TH (BS kennt alle Prioritäten und Wartebeziehungen)

## Implementierung von Semaphoren
Problem: BS muss atomare Veränderungen der Synchronisationsvariablen unterstützen
Idee: verwende Hardware-Synchronisation
- Einschalten/Ausschalten [[Unterbrechungsbehandlung]] (Semaphor im privilegiertem Kern implementiert)
--> Ok für Einprozessorsysteme (keine Präemption und somit keine [[Nebenläufigkeit]] im Semaphor bei deaktivierten Unterbrechungen)
--> nicht Ok für Mehrprozessorsysteme ([[Threads]] können auf mehreren CPUs nebenläufig ausführen, trotz abgeschalteter Interrupts)

Java-Befehl: 
- CLI; // Clear Interrupts (keine Interrupts ab hier)
- SEI; // SEt Interrupts (Interrupts wieder erlauben)

__Faire Spin-Locks__
z.B. Ticket-Lock mit Fetch&Add auf __Ein- oder Mehrprozessorsystemen__

### erweiterte Datenstruktur
drei Elemente
- integer (binary) value
- queueType queue
- __TicketLock lock__ --> koordiniert Aktualisierung des Semaphores

--> Initialisierung: Semaphore S <-- (k, leere Menge); S.lock <-- free

### Java Implementierung
S.lock.acquire(); --> faires aktives warten (aber nur kurz)
S.lock.release();

### Bsp. Koordination: Mergesort mit Semaphor
![[Mergesort mit Semaphor.png]]
Synchronisationsprobleme koordinieren zusätzlich Zugriffsordnung
Semaphoren ermöglicht einfache Implementierung vieler Synchronisationsparadigmen

## KA mit Semaphoren
```java
public class SemaphoreDemo implements Runnable {
	static Semaphore semaphore = new Semaphore(1);
	public void run() {
		semaphore.acquire();
		//KA
		semaphore.release();
	}
	public static void main (String[] args) {
		new Thread(new SemaphoreDemo()).start();
		new Thread(new SemaphoreDemo()).start();
	}
}
```