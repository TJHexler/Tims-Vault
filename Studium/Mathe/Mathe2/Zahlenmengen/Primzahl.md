---
tags: Uni Mathe
VL-Date: 12.04.23
---
# Primzahlen
## Definition 1.35 Was sind Primzahlen?
Eine natürliche Zahl p ≥ 2 heißt Primzahl, falls D(p) = {1, p} ist.

## Lemma 1.36
Jede natürliche Zahl $n >= 2$ ist ein Produkt von Primzahlen. (Beweis über vollständige Induktion siehe Skript)

## Theorem 1.37 Fundamentalsatz der Arithmetik
Jede natürliche Zahl n ≥ 2 lässt sich bis auf die Reihenfolge der Faktoren auf genau eine Weise als Produkt von Primzahlen schreiben.
## Theorem 1.38 Satz von Euklid
Es gibt unendlich viele Primzahlen
### Beweis
Wir nehmen an, es gäbe r verschiedene Primzahlen p1, p2, . . . , pr. Wir konstruieren weitere Primzahlen. Dazu zerlegen wir die Zahl p1p2 . . . pr + 1 in Primfaktoren p1p2 . . . pr + 1 = q1q2 . . . qs. Wir zeigen durch einen Widerspruchsbeweis, dass pi 6= qj ist für 1 ≤ i ≤ r, 1 ≤ j ≤ s.
Wäre fur ein i = i0 und ein j = j0 pi0 = qj0, dann wäre pi0|q1 . . . qs und damit pi0|(p1 . . . pr + 1).
Es würde folgen, dass pi0|1, was nicht sein kann. Daher sind q1, . . . , qs weitere Primzahlen, die wir der Liste p1, p2, . . . , pr hinzufugen können.