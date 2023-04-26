---
tags: Uni Mathe
VL-Date: 12.04.23
---
# 1.31 Peano-Axiome
In der Mathematik werden aus gegebenen Aussagen mit Hilfe logischer Schlussfolgerungen neue Aussagen gewonnen, die Sätze. Dieser Prozess muss irgendwann beginnen. Am Anfang müssen Tatsachen stehen, die als wahr angenommen werden, ohne dass diese bewiesen werden. Diese Grundtatsachen nennt man Axiome. Giuseppe Peano (1858-1932) hat 1889 das folgende Axiomensystem aufgestellt, wodurch natürliche Zahlen charakterisiert werden.

## Definition 1.31 Peano-Axiome
Die natürlichen Zahlen bilden eine Menge $N$, auf der eine Abbildung $f$, die jedem n einen Nachfolger zuordnet; $f : N → N$ erklärt ist, die folgende Eigenschaften besitzt: 
- $∃ !1 ∈ N : 1 \notin f(N)$, d.h. es existiert genau eine Zahl, die nicht Nachfolger einer anderen Zahl ist. 
- Die Abbildung $f$ ist injektiv, d.h. aus $f(n1) = f(n2)$ folgt $n1 = n2$. 
- Ist $M ⊆ N$ und gilt
	a) $1 \in M$
	b) aus $n \in M$ folgt $f(n) \in M$
	dann ist M = N.
### Bemerkung
- Die Zahl 1 ist die kleinste natürliche Zahl. Das ist Konvention. Man könnte auch mit der 0 beginnen. Um die 0 einzubeziehen führt man $N_0 = N ∪ \{ 0\}$ ein.
- Das dritte Axiom wird auch Induktionsaxiom genannt. Es bildet die Grundlage für ein Beweisverfagen, das vollständige Induktion genannt wird.