---
tags: Uni Syskon
---
# Dekkers-Algorithmus
Lösung der starken Formulierung des KA-Problems __für nur 2 Prozesse/[[Threads]]__
Annahmen: gemeinsamer Hauptspeicher, atomares Lesen, atomares schreiben, sequentielle Konsistenz, schwach faires [[Scheduling]]

## Überprüfung durch Model-Checking
Tool, beschreibe Algorithmus und Korrektheitsbedingungen --> Model-Checker zählt alle Zustände auf und überprüft, ob Eigenschaften erfüllt sind
- liefert Gegenbeispiel, wenn Eigenschaft verletzt
- terminiert ohne Fehler, wenn Eigenschaften erfüllt
- terminiert nicht bei keiner Aussage

## Ansatz
### Idee 1
![[Dekkers Algorithmus Idee Ansatz 1.png]]
erfüllt: kein wechselseitiger Ausschluss, Freiheit von Verklemmung
Aber: Aushungern möglich (p muss nicht unbedingt in KA, p führt nie turn = 2 aus --> q kommt nie in KA)
--> Ansatz erfüllt nur schwache Formulierung des KA-Problems
### Idee 2
warte nicht auf Thread, der gar nicht in KA will, um nicht zu verhungern
![[Dekkers Algorithmus Idee Ansatz 2.png]]
erfüllt: keine Verklemmung
Aber: kein wechselseitiger Ausschluss, Aushungern selbst bei fairer Ausführung möglich (await immer nur dann, wenn KA vom anderen Thread betreten)
### Idee 3
vertausche Zeilen 2 und 3 miteinander
erfüllt: wechselseitigen Ausschluss
Aber: Verklemmung möglich (wantp=wantq=true, beide in await Zeile)

## Der Algorithmus
![[Dekkers Algorithmus.png]]
Variable turn löst Verklemmung in deterministischer Weise auf --> falls beide in KA wollen, wechseln sie sich ab --> __kein Aushungern__

Invariante 1: wenn p (q) im KA --> wantp=true (wantq=true)
Invariante 2: sowohl p und q verschachtelte Aufrufe in Zeile 3 bis 7 --> keine Änderung von turn

mit Invarianten können wir beweisen:
- erfüllt wechselseitigen Ausschluss (4.2.22)
- erfüllt keine Verklemmung (4.2.23)
- erfüllt kein Aushungern (4.2.25)