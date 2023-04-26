---
tags: Uni Syskon
---
# Monitore
von Per Brinch Hansen
__objektorientierter Ansatz__:
- gemeinsame Daten im Zustand des Monitors-Objekts gekapselt
- Manipulation der Daten nur über Methoden des Monitor-Objekts
- Nur __ein__ Thread kann gleichzeitig ausführen

__kein aktives Warten__, nur ein Thread führt Methodenaufruf des Monitors aus , weitere [[Threads]] blockieren, faires Warten verhindert Aushungern, Veränderung des Objektzustandes (gemeinsame Daten) erfolgt ausschließlich über Methodenaufrufe des Monitor-Objekts, Initialisierungsroutine definiert Initialzustand

Bsp.: 
```java
monito Example {
	operation O1() {...}
	operation O2() {...}
}
```
![[Monitor Bsp.png]]
--> keine Verschachtelung von p1 und q1

## Bedingungsvariablen
Koordination: [[Threads]] warten auf Ereignisse bzgl. Bedingungsvariablen
- condition c: faire __Warteschlange__ für Ereignisse bzgl. c
- c.wait(): Thread wartet auf Ereignis bzgl. c --> blockiert in Warteschlange von c
- c.signal(): generiert Ereignis bzgl. c --> blockierter Thread kann fortfahren
- c.empty() = true: keine blockierten [[Threads]] bzgl. c

## Monitor in Java
Schlüsselwort __synchronized__
Jedes Objekt in Java ist mit einem __Monitor-Lock__ (intrinsisches Lock) assoziiert;
Nur ein Thread kann aktiv in einem synchronized-Block ausführen;
Bei Eintritt in Sync.-Block wird entweder __Monitor-Lock__ erworben, oder der Thread blockiert;
Bei Austritt wird Monitor-Lock wieder freigegeben;
Bereits erworbenes __Monitor-Lock__ ermöglicht Eintritt in andere Synchronized Blöcke desselben Objekts (Bsp.: op1() ruft opt2() auf)

notifyall() --> alle [[Threads]] wieder ablauffähig
Java erzwingt nicht die Eigenschaften eines Monitors:
- Variablen in Monitor-Klasse können public sein
- Synchronisation wird nicht erzwungen
	- nicht synchronisierte Methoden können auf Variablen im Monitor zugreifen (Schutz der Variablen durch Monitor wird umgangen
--> __Reantrant Locks__