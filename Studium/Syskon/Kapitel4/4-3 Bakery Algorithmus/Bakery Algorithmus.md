---
tags: Uni Syskon
---
# Bakery Algorithmus
Lösung der starken Formulierung des KA-Problems für __beliebige Anzahl von [[Threads]]__ von Leslie Lamport
Annahmen: gemeinsamer Hauptspeicher, atomares Lesen, atomares schreiben, sequentielle Konsistenz, schwach faires [[Scheduling]]
## naiver Ansatz
![[Bakery Algorithmus naiver Ansatz.png]]
erfordert Atomizität von 2 trotz mehrerer Zugriffe (lesen und schreiben) auf globale Variable number

wenn Zeile 2 atomar --> solange Thread in 3 bis 6 ausführt, erhält nachfolgender Thread größere Nummer; wegen 4: Ein Thread kann erst in KA, wenn alle [[Threads]] mit kleineren Nummer 6 ausführen
wenn Zeile 2 nicht atomar --> für $p_i$ und $p_j$ number(i) = number(j) möglich 
--> wähle __eindeutige__ Nummer

## totale Ordnung <<
(Nummer, Thread-Identität): (1,2) << (1,3), aber (2,2) >> (1,3)

## naiver Ansatz mit totaler Ordnung <<
![[Bakery Algorithmus naiver Ansatz mit totaler Ordnung.png]]
Problem: Sichtbarkeit des Updates von number(i) für $p_j$ erforderlich für den Fall number(i) = number(j) und i > j

--> __Race-Condition__: mehr als ein Thread im KA möglich!

## korrekter Algorithmus
![[Bakery Algorithmus.png]]
erfüllt:
- wechselseitiger Ausschluss
- keine Verklemmung
- kein Aushungern