---
tags: Uni Syskon
---
# Prozesswechsel
**Freiwillig**
- wartet auf notwendige Ressourcen (E/A) 
- warten durch anderen Prozess gesetzte Sperre
- Systemaufruf: sleep
**Präemption**
- ablaufen des Zeitquantums (Uhr-[[Unterbrechungsbehandlung]])
- Prozess mit höherer Priorität bereit

Zeitpunkte für Prozesswechsel: 
- Uhren-UBR (Timer Interrupt)
- E/A-UBR
- Speicherfehler (Exception)
- Systemaufruf (Software-Interrupt)
- Fehler (Exception)

Freiwilliger Wechsel bei E/A --> höhere CPU-Auslastung (Wartezeit wird sinnvoll ausgenutzt)

## Lebenszyklus eines Prozesses
### einfache Sicht
![[LebenszyklusProzessEinfach.png]]
### Elemente zur Auswahl von Prozessen
Warteschlange mit nicht aktiven Prozessen (FIFO oder Prioritätswarteschlange) --> Ziel: möglichst wenig Befehle zur Auswahl ausführen --> günstiges [[Scheduling]]
### Erweiterung des Modells
zusätzliche Zustände: neu, blockiert, terminiert
![[Prozesszustände.png]]
Problem: nicht ausreichend Speicher pro Prozess vorhanden --> **Auslagern** --> freier Speicher von Prozessen nutzbar
--> neuer Zustand: **suspendiert**
![[ProzesszuständeVollständig.png]]
Prozesswechsel = Übergang: aktiv --> beliebiger anderer Zustand
### Prozesshierarchie
starten eines Prozesses: Shell, graphische Nutzerschnittstelle, aus Benutzerprogramm
Eltern-Kind-Abhängigkeit (Hierarchie): neuer Prozess (Kind) wird immer von einem anderen Prozess (Parent) gestartet