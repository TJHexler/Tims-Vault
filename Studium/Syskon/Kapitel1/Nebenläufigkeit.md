---
tags: Uni Syskon
---
# Nebenläufigkeit
Aktivitäten gleichzeitig ausführen, geht nur ohne kausale Abhängigkeit (A kommt vor B)

## sequentielle und nebenläufige Programme
Der Begriff "parallel" bezeichnet typischerweise echte Parallelität. Der Begriff "nebenläufig" bezeichnet mögliche Parallelität, d.h. echte Parallelität und Quasiparallelität.

### sequentielles Programm
- alle Instruktionen werden sequentiell ausgeführt

### [[nebenläufiges Programm]]
- engl. concurrent Program
- besteht aus einer Menge sequentieller Programme, die parallel ausgeführt werden können 

## Vorteile der Nebenläufigkeit
### Ausnutzung mehrerer Prozessoren
- sequentielles Programm kann bei 100 Prozessoren maximal 1% Rechnerkapazität nutzen
- nebenläufige Programme können potenziell gesamte Kapazität nutzen, d.h. **verbesserter Durchsatz** (selbst bei Einprozessor-Systemen durch Quasiparallelität)
### einfachere Modellierung
- reale Prozesse bestehen oft aus nebenläufigen Aktivitäten
- "Natürliche" Modellierung, bei der einzelne Aktivitäten durch sequentielle Programme realisiert werden

## Herausforderungen der Nebenläufigkeit
- erfordert Kommunikation + Synchronisation zwischen Prozessen
- Probleme sind häufig situations- und zeitabhängig --> schwierig zu reproduzieren, diagnostizieren und korrigieren
### Race Condition
- Ergebnis einer Berechnung hängt vom zeitlichen Verhalten einzelner Operationen ab

![[einfaches Nebenläufigkeitsbeispiel.png]]
### Deadlocks Verklemmungen
- Menge von Prozessen blockieren sich zyklisch gegenseitig

![[Nebenläufigkeit Beispiel.png]]