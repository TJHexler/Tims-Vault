---
tags: Uni Syskon
---
# RMW-Befehle

### Bsp. atomare Read-Modify-Write-Befehle
Test&Set - gibt Wort von Variable aus und setzt ihn auf 1 wenn er 0 war
Compare&Swap - if i = erwartet then i = neu und return true, sonst return false
Fetch&Add - erhöhe Wert atomarer Variablen um geg. Wert, liefere alten Wert unmittelbar vor Addition zurück

## Vorteile Atomare RMW-Befehle
- anwendbar für beliebig viele [[Threads]]
- einfach und leicht zu verifizieren
- sehr effizient bei __geringer Lock-Contention__ (keine Wechsel Kernel/User-Mode des eintretenden [[Threads]] --> geringe Latenz bis zum Eintritt in KA)

## Nachteile Atomare RMW-Befehle
- __hohe Lock-Contention --> Busy-Waiting kostet 100% CPU-Last__
- bei nicht fairem [[Scheduling]] (unterschiedliche Threadprioritäten) Aushungern möglich
-->
	- Thread mit niedrigster Priorität hindert Thread mit hoher Priorität an Beitritt in KA (__Prioritäten-Inversion__: andersrum)
	- beachte: __busy-waiting = Thread ausführungsbereit__ --> Scheduler des [[Betriebssystem]] führt Thread der wartet und niedrige Prio aus
	- Szenario: [[Threads]] TH und TN
		- TH blockiert im nicht KA --> TN kommt dran und betritt KA --> TH wird nach E/A wieder ausführungsbereit --> BS unterbricht TN, da TH höhere Priorität --> TH möchte KA betreten und führt Präprotokoll aus - Spinning auf Lock (while Loop)
--> TH andauernd ausführungsbereit, kann KA aber nicht betreten --> __TH verhungert__