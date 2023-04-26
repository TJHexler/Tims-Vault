---
tags: Uni Mathe
---
# 1.4 Äquivalenzrelationen
## Definition 1.4.1
Sei $M$ eine Menge und $R$ eine [[Relation]] auf $M × M$. Dass zwei Elemente $a, b$ von $M$ in [[Relation]] stehen, drücken wir durch die Schreibweise $a \sim b$ aus. Die [[Relation]] heißt Äquivalenzrelation, wenn sie die drei folgenden Eigenschaften besitzt:
1. __Reflexivität__: $\forall a \in M: a \sim a$
2. __Symmetrie__: $\forall a, b \in M: a \sim b \Rightarrow b \sim a$
3. __Transitivität__: $\forall a, b, c \in M: (a \sim b \wedge b \sim c) \Rightarrow a \sim c$
## Äquivalenzklassen
Fur eine Äquivalenzrelation ∼ ist die Äquivalenzklasse eines Elements $x ∈ M$ durch $\left[ x \right] := \{y ∈ M | y ∼ x\}$ definiert.

## Satz 1.4.2
Ist $M$ eine Menge und $∼$ eine Äquivalenzrelation auf $M$, so gilt, dass die Menge der Äquivalenzklassen $\{ \left[ x\right] | x ∈ M\}$ eine disjunkte Zerlegung oder Partition von M bildet, d.h. es gilt $M = \cup_{x∈M} \left[ x \right]$ und je zwei Äquivalenzklassen stimmen entweder überein oder haben leere Schnittmenge. Umgekehrt, ist $\{ M_j | j ∈ J\}$ eine disjunkte Zerlegung einer Menge $M$, d.h. es gilt $M_j ∩ M_k = ∅$ falls $j ̸= k$ und $M = \cup_{j \in J} M_j$ , so ist durch $x ∼ y ⇔ ∃j ∈ J : x, y ∈ M_j$ eine Äquivalenzrelation auf $M$ definiert.