---
tags: Uni Syskon
---
# Verarbeitungsmodelle

## Grundprinzipien, wie Verarbeitung erfolgt
- beteiligte Komponenten und ihre Rollen
- Kommunikationsmuster zwischen den Komponenten

## Produzent/Konsument-Modell
- Produzent erzeugt Daten und sendet diese zum Konsumenten
- Konsument erhält und verarbeitet Daten
- Unidirektionale Kommunikation

## Pipeline-Modell
- Verallgemeinerung vom Produzent/Konsument-Modell
- Prozesse sind sowohl Produzent, als auch Konsument
- Prozesse über unidirektionale Kommunikationskanäle verbunden

Bsp: Kamera -> Encoder -> Decoder -> Anzeigegerät

## Client/Server-Modell
- Server bietet Dienste einer vorher unbekannten Anzahl von Klienten an
- Klient nutzt angebotene Dienste
- Interaktion: Auftrag/Antwort
- Server können Klienten anderer Dienste sein
- Dienste sind [[Threads]]

Bsp: Dateidienst(NFS, AFS), Verzeichnisdienst(DNS), WWW, Suchmaschinen
Bsp: WWW-Server verwendet einen Anwendungsserver, um auf Datenbank zuzugreifen

![[Server Client Modell.png]]


