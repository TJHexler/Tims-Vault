---
tags: Uni Syskon
---
# Spin-Locks
Lösung der __schwachen__ oder __starken Formulierung__ des KA-Problems für __beliebig viele [[Threads]]__
einfache Spin-Locks: Aushungern möglich
Ticket-Locks: verhindern auch Aushungern (bei fairem [[Scheduling]])
Annahmen: atomarer Read-Modify-Write-Befehl, gemeinsamer Hauptspeicher, sequentielle Konsistenz, schwach fairer Scheduler

## was sind Spin-Locks
- RMW-primitive erlauben Implementierung von Sperren (Lock)
- Akquirieren der Sperre vor[[Kritischer Abschnitt]]: lock.aquire()
	- nur genau ein Prozess kann Sperre halten (--> wechselseitiger Ausschluss)
	- Sperren erfolgt im Präprotokoll
- Prozess, der Sperre hält, gibt Sperre nach KA wieder frei: lock.release() 
	- nur Prozess der Sperre hält, kann Sperre freigeben (unterschied zu Semaphoren)
	- freigeben erfolgt im Postprotokoll
- Warten auf Sperre erfolgt bei RMW durch __Busy-Waiting__
	- Vorteil: geringe Latenz um freie Sperre zu sperren
	- Nachteil: CPU-Verschwendung, wenn viele [[Threads]] um Lock "streiten" (unterschied Semaphoren: kein aktives warten)
- Java Implementierung mit getAndSet oder CompareAndSwap bei 4.4.9

## Eigenschaften der bisherigen Lösungen
lösen nur __schwache Formulierung__ des KA-Problems (wechselseitiger Ausschluss und keine Verklemmung, aber Aushungern möglich)
Aushungern selbst bei fairem Scheduler: zufällig RMW-Befehl immer zu falschen Zeit --> verlässt while-Schleife nie. Eigenschaft muss für beliebige Ausführungssequenz gelten!

## Fairer Beitritt in KA: Ticket-Locks
mithilfe von __Fetch-and-Add__:
- Idee ähnlich zu Bakery-Algorithmus
1. [[Threads]] ziehen Nummer (eindeutig, streng monoton steigend) --> kann durch keinen anderen Thread dauerhaft verhindert werden
2. [[Threads]] treten in KA in Reihenfolge der Ticketnummer

mit Fetch&Add leichter zu implementieren als Bakery-Algorithmus(der nur atomare Lese- und Schreibbefehle verwendet) - Implementierung 4.4.16
Integer kann nur __endlich viele Ticketnummern__ abbilden (Integer: 32 bit --> $2^32$ Tickets --> Kollisionsmöglichkeit, wenn mehr als $2^32$ [[Threads]] gleichzeitig Nummer ziehen (reicht aber normal aus, sonst AtomicLong (64bit) verwenden)
