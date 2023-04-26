---
tags: Uni Syskon
---
# Unterbrechungen (Interrupts)
## Unterbrechungszyklus
Prozessor überprüft, ob **Unterbrechung (UBR)/Interrupt(INT)** signalisieren wird, falls keine UBR vorliegt holt Prozessor nächsten Maschinenbefehl und führt ihn aus. Ansonsten wird Kontrolle an **UBR-Routine (INT Service Routine ISR, Interrupt Handler) übergeben
![[Unterbrechungszyklus.png]]

## Unterbrechungen nur zwischen Maschinenbefehlen
beachte: [[Betriebssystem]] ist selbst ein Programm --> UBRs möglich, aber privilegiertes Programm (kann Interrupts deaktivieren)(es gibt aber auch UBRs, die das BS deaktivieren können)

BS bestimmt, wie Interrupt behandelt wird

## Arten von Interrupts
Hardware-Interrupts: 
- asynchron zum Prozess
- Bsp.: Tastendruck(E/A), Timer, etc.
Software-Interrupts: 
- Maschinenbefehl INT (x86)
- Bsp.: Systemaufrufe (Datei öffnen, Prozess starten, etc.)
Ausnahmen(Exceptions)/Prozessor Interrupts:
- Bsp.: Speicherzugriffsfehler, Division durch Null

## [[Betriebssystem]] nutzt Interrrupts für
- Kontrolle des Ablaufs von Prozessen
- Systemaufrufe durch Anwendungen (Aufruf von im BS implementierten systemnahen Funktionen)
- effiziente Interaktion mit E/A-Geräten
- virtuelle Speicherverwaltung
- Fehlerbehandlung
![[Interruptnutzen.png]]