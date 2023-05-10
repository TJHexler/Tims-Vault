---
tags: Uni Mathe
---
# 2.4 Körper
## Definition 2.4.1
Ein kommutativer Ring mit Eins heißt __Körper__, wenn jedes Element außer das neutrale Element 0 der Addition ein multiplikatives Inverses besitzt.

## Axiome für einen Körper
- Die Addition ist assoziativ: ∀a, b, c ∈ K : (a + b) + c = a + (b + c)
- Es gibt ein neutrales Element 0 bezüglich der Addition: ∀a ∈ K : a + 0 = a
- Zu jedem Element in K gibt es ein inverses Element bezüglich der Addition: ∀a ∈ K ∃b ∈ K : a + b = 0
- Die Addition ist kommutativ: ∀a, b ∈ K : a + b = b + a.
- Die Multiplikation ist assoziativ: ∀a, b, c ∈ K : (a · b) · c = a · (b · c)
- Es gibt ein neutrales Element 1 bezüglich der Multiplikation: ∀a ∈ K : a · 1 = a
- Zu jedem Element in K \ {0} gibt es ein inverses Element bezüglich der Multiplikation: ∀a ∈ K ∃b ∈ K : a · b = 1.
- Die Multiplikation ist kommutativ: ∀a, b ∈ K : a · b = b · a
- Es gilt das Distributivgesetz: ∀a, b, c ∈ K : a · (b + c) = a · b + a · c

Ein Körper K ist somit eine abelsche Gruppe bezüglich der Addition und K \ {0} ist eine abelsche Gruppe bezüglich der Multiplikation. Ein Körper ist ein Zahlenbereich, in dem wir addieren, subtrahieren, multiplizieren und dividieren können, so wie wir dies beim Rechnen mit rationalen oder reellen Zahlen gewohnt sind.

#### Beispiele für Körper 2.4.2
- Die rationalen Zahlen mit der üblichen Addition und Multiplikation
- Der Körper $\mathbb{R}$ dargestellt durch unendliche Dezimalbrüche
- Die komplexen Zahlen $\mathbb{C}$ (Die komplexen Zahlen enthalten die reellen Zahlen als *Teilkörper*)
- Der Körper $\mathbb{Z}_2$ mit zwei Elementen

## Satz 2.4.3
In einem Körper gibt es keine Nullteiler: Sei $K$ ein Körper und seien $a, b \in K$. Falls $ab=0$, dann gilt $a=0$ oder $b=0$.

## Bemerkung
Der Ring der reellen Polynome in einer Variablen ist ein kommutativer Ring mit Eins. In ihm gibt es keine Nullteiler, aber er ist dennoch kein Körper. Beides folgt aus der Tatsache, dass sich beim Multiplizieren zweier Polynome sich die Grade der Polynome addieren.