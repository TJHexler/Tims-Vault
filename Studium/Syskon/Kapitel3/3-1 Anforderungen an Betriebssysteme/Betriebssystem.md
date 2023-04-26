---
tags: Uni Syskon
---
# Betriebssystem
- Menge von Dienstprogrammen
- Schnittstelle zwischen Anwendungen und Hardware
- Ressourcenverwaltung 
- ermöglicht und kontrolliert **verschachtelten Ablauf von Prozessen**
--> übergibt Kontrolle über den Prozessor an andere Programme

## Betriebssystem-Kern
- Untermenge des Betriebssystem im Hauptspeicher
- enthält zentrale Betriebssystem-Funktionalität
	- Hardwareschnittstelle
	- Prozessverwaltung ([[Scheduling]])
	- Speicherverwaltung
	- Interprozesskomunikation
- verantwortlich für die [[Granularität]] [[Nebenläufigkeit]] Ausführungen

## serielle Verarbeitung
nur ein Programm kann auf der Rechnerarchitektur laufen
--> erfordert:
- manuelles Ausbringen auf das System (übersetzen, linken)
- Programm muss selbst angeschlossene Geräte steuern und integrieren
--> komplex und ineffizient
--> Prozesskonzept für effiziente Gestaltung von grundlegender Bedeutung

## Batch-Systeme
ermöglichen automatisierte Unterstützung der Ausbringung mehrerer Programme
Batch (Stapel): 
- fasst mehrere Programme zusammen und kontrolliert deren Ablauf auf dem System
[[Monitor]]: 
- übernimmt Systemsteuerung und Ressourcenkontrolle
- steuert den Ablauf der Programme
	- Ausbringung der Programme auf dem System
	- Steuerung von Hardwaregeräten
	- Speicherverwaltung
	- [[Scheduling]] (nur bei [[Multiprogrammierung]])
früher: Uniprogrammierung - Programme in sequentieller Reihenfolge --> immer nur ein Programm im Hauptspeicher
--> Problem: sehr ineffizient - selbst für Uniprozessorsysteme (Programme müssen häufig auf Eingabe/Ausgabe-Geräte (E/A) zugreifen --> deutlich langsamer als Prozessor --> viel Leerlauf --> niedrige Auslastung)

## Recap
- spezielle Systemkonzepte zur effizienten Nutzung komplexer Rechnerarchitekturen nötig
- Prozesse kümmern sich nicht selbst um das Management der Systemressourcen
- [[Betriebssystem]]/Systemsoftware bietet wohldefinierte Schittstellen zum Zugriff auf Systemressourcen 
	- Systembibliothek: Dateizugriff, Netzwerk, Shared Memory, etc.
	- Systemtools: Kommandos in einer Shell
- [[Betriebssystem]] verwaltet die Ressourcen und entscheidet, welcher Prozess abläuft
- ermöglicht dynamische Erstellung/Terminierung neuer Prozesse
- [[Betriebssystem]] bietet Schutzmechanismen - Isolation und Zugriffsmechanismen von Prozessen