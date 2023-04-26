---
tags: Uni Syskon
---
# Kritischer Abschnitt
Annahme: alle [[Threads]] eines nebenläufigen Programms kommunizieren über gemeinsamen Speicher
Problem: Programm für Kontostandänderung mit jedem Update durch eigenen Thread --> evtl. Resultat abhängig von Verschachtelung (__Race-Condition__)(z.B. __Lost-Update__)
--> vermeide Verschachtelung im KA (kritischen Abschnitt)

## Ablauf aus Sicht eines [[Threads]]
1. nicht KA
2. Präprotokoll - stellt sicher: nur ein Thread im KA --> keine Race Condition über gemeinsame Ressourcen
3. KA
4. Postprotokoll
immer noch beliebige Verschachtelungen im nicht KA möglich

## Korrektheitskriterien KA: Mindestanforderungen
### Definition 4.1 (schwache Formulierung)
Jede Lösung zum Problem des kritischen Abschnitts muss folgenden Eigenschaften genügen: 
1. Wechselseitiger Ausschluss (Mutual Exclusion): Keine Verschachtelung zweier [[Threads]] bzgl. Befehlen des kritischen Abschnitts. 
2. Keine Verklemmung (Deadlock): Falls mehrere [[Threads]] versuchen, den kritischen Abschnitt zu betreten, wird ein (beliebiger) Thread letztendlich erfolgreich sein.
Annahme: KA garantiert Fortschritt --> kein unendliches Verweilen im KA erlaubt
Verklemmung: jeder Thread wartet auf Ergebnis eines anderen Threads (Bsp.: schlechtes Präprotokoll, sendet z.B. Antwort erst nach Erhalt der Antwort auf eigene Frage)
--> stellt Konsistenz der Daten sicher und Anwendung kann insgesamt voranschreiten

Problem: __kein individueller Fortschritt garantiert__
Bsp.: viele kontinuierliche Anforderungen, Anforderung eines Kunden wird möglich nie beantwortet --> __Aushungern__

### Definition 4.2 (starke Formulierung KA)
Jede Lösung zum Problem des kritischen Abschnitts erfüllt zusätzlich zum wechselseitigen Ausschluss (1) und Freiheit von Verklemmung (2) folgende Eigenschaft: 
3. Kein Aushungern. Wenn ein Thread den kritischen Abschnitt betreten möchte, so wird er ihn letztendlich betreten.

Beachte: selbst wenn [[Betriebssystem]]-[[Scheduling]] faire Ausführung von Threads sicherstellt, ist zusätzlicher Aufwand nötig, um Aushungern zu vermeiden. Die Vermeidung von Aushungern muss für jede beliebige schwach faire Ausführung des BS-Schedulers sichergestellt werden.