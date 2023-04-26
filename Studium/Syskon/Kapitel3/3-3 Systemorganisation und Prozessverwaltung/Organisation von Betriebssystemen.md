---
tags: Uni Syskon
---
# Organisation von Betriebssystemen
- [[Betriebssystem]] beinhaltet zumeist verwendete BS Funktionalität
- Hardware geschützt durch Kern
- Anwendungen interagieren nur über wohldefinierte Schnittstellen und Systembibliotheken
![[BSKern.png]]

## Monolithische Organisation
traditionelles BS verwendet monolithische Struktur
- Menge von Prozeduren
- Jede Prozedur kann jede andere aufrufen
- heute nach wie vor vorherrschende Organisation
![[monolithische Organisation.png]]

## Mikrokern (Micro Kernel)
![[Mikrokern.png]]

## Systemaufrufe
### Grundkonzept:
![[SystemaufrufGrundkonzept.png]]
### Übersicht (POSIX)
Prozesse:
- fork, exeve: Prozess starten
- wait4, waitpid: auf Kindprozess warten
Dateien:
- open, close: Datei öffnen, schließen
- read, write: offene Datei lesen, schreiben
Sockets (Netzwerkkommunikation): 
- socket: Socket erzeugen
- bind: binden an Port
- accept: eingehende Verbindungsanfrage akzeptieren
### detaillierter Ablauf eines Systemaufrufs
![[Ablauf Systemaufruf.png]]
