---
tags: Uni Syskon
---
# Multiprogrammierung/Multitasking
effizientere Auslastung des Prozessors durch nebenläufige Ausführung von mehreren Programmen
erfordert zusätzliche Konzepte:
- Prozesskonzept: Verwaltung des Zustands eines Programms
- Unterbrechung der Ausführung eines Prozesses: [[Unterbrechungsbehandlung]]
- Effiziente Steuerung von E/A-Geräten: Unterbrechungsgesteuerte E/A, Direct Memory Access (DMA)
- Verwaltung gemeinsamer Ressourcen: virtueller (Haupt-)Speicher, Sekundärspeicher (Dateien)
- [[Scheduling]]:Bestimmung des Zeitpunktes der Ausführung eines Prozesses

## Time-Sharing
unterstützt zusätzlich die Interaktion einer Anwendung mit seiner Umwelt
Bsp.: alle Anwendungen mit Nutzerinteraktion (Konsole, Spiele, etc.)


--> Batchbasierte Multi-Programmierung nicht geeignet! --> optimiert ausschließlich Prozessorauslastung
## Anforderungen an [[Scheduling]]
Optimierungsziel des Prozess-Schedulings: **kurze Antwortzeit für alle Prozesse**
zusätzliche Anforderung an [[Scheduling]]: [[Fairness]]
weitere wichtige Anforderung: **Echtzeitfähigkeit**
- ermöglicht Interaktion von Prozessen mit physischer Umgebung
- Ereignisse erfordern Reaktion in Echtzeit (rechtzeitig)
	- Multimedia:Milisekunden
	- Überwachung, Steuerung & Regelungen, Cyber-Physical-Systems: teilweise Mikrosekunden
- Korrektheit des Systems hängt nicht nur vom logischen Resultat ab
- Zeitpunkt der ausgeführten Berechnungen ist wichtig (jede Berechnung hat eine Zeitschranke **Deadline**, sonst Gefährdung der Sicherheit(safety))
- **harte** und **weiche** Anforderungen
- Umsetzung in Reallife: **Echtzeitbetriebssystem** --> garantiert echtzeitkritischen Prozessen Zugriff auf CPU innerhalb geforderter aufgabenspezifischer Zeitspannen
--> zusätzliche Anforderung: **Echtzeitscheduling**
Optimierung der Antwortzeit wie bei Time-Sharing nicht ausreichend (minimale Antwortzeit ist nicht das Ziel, sondern garantierte Antwortzeit)
Echtzeitsysteme werden in VL nicht weiter betrachtet:)
