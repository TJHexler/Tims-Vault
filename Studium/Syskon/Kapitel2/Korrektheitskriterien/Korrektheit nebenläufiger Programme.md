---
tags: Uni Syskon
---
# Korrektheit nebenläufiger Programme
[[Nebenläufigkeit]]
## Korrektheit: Sicherheit (safety)
### Definition 2.3
Für eine ***Sicherheitseigenschaft*** eines Programms gilt: Die Sicherheitseigenschaft gilt in jedem möglichen Ausführungszustand des Programms.
### Beispiele Sicherheitseigenschaften
1. Pro Vorstellung werden maximal n Kinokarten vergeben. 
2. Pro Vorstellung wird jeder Sitz nur einmal vergeben. 
3. Jede Antwort des Systems enthält eine Karte oder eine Ablehnung. 
4. Eine Anfrage wird nur abgelehnt, wenn es keine freien Karten gibt. 
5. Eine Karte wird nur vergeben, wenn eine Kontonummer angegeben wurde.
## Korrektheit: Lebendigkeit (liveness)
"sicherstellen, dass letztendlich etwas gutes passiert"
### Definition 2.4
Für eine Lebendigkeitseigenschaft gilt: Für jeden Zustand eines Programms gibt es eine Fortsetzung der Ausführung, welche die Eigenschaft in endlich vielen Schritten erfüllt.

- definiert keine obere Zeitschranke
- die Eigenschaft "Antwort in XX Sekunden wäre eine Sicherheitseigenschaft"
### Beispiel Lebendigkeitseigenschaft
1. Jede Anfrage wird vom System schließlich beantwortet