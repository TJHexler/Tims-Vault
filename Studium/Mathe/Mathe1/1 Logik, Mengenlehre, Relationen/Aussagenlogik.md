---
tags: Uni Mathe
---
# 1.1 Aussagenlogik
Eine *Aussage* ist ein sprachliches Gebilde, von dem es sinnvoll ist, zu fragen, ob es wahr oder falsch ist.
Jeder Aussage kann man einen Wahrheitswert zuordnen. Dabei kommt es nicht darauf an, ob wir tatsachlich in der Lage sind, richtig über den Wahrheits-wert zu entscheiden. Es gibt sehr viele mathematische Aussagen, von denen (noch) niemand weiß, ob sie wahr oder falsch sind.
In der Aussagenlogik geht es darum, einzelne Aussagen miteinander zu verknüpfen. Dabei betrachten wir die einzelnen Aussagen zunächst nicht mehr im Detail, sondern wir sehen sie im Folgenden nur als Bausteine, als sogenannte Elementaraussagen, an, aus denen wir größere Aussagen, sogenannte aussagenlogische Formeln, aufbauen wollen. Die einzelnen Aussagen, die an einer solchen Formel beteiligt sind, bezeichnen wir in diesem Abschnitt deshalb nur noch mit einem Buchstaben wie $p, q$, etc. Die Verknüpfungen heißen logische Junktoren.
## Negation
Die einfachste Möglichkeit, eine solche aussagenlogische Formel zu bauen, ist die Negation, also die Verneinung einer Aussage. Die Verneinung der Aussage “Es regnet.” ist natürlich die Aussage “Es regnet nicht.” Die __Negation__ einer Aussage $p$ bezeichnen wir mit $¬p$. Die Aussage $¬p$ (gesprochen “nicht p”) ist definiert als die Aussage, die dann wahr ist, wenn p falsch ist und die dann falsch ist, wenn p wahr ist. Das kann man in Form einer Tabelle ausdrücken. Eine Tabelle, die den Wahrheitswert einer aussagenlogischen Formel in Abhängigkeit der Wahrheitswerte der beteiligten Einzelaussagen angibt, nennt man __Wahrheitstafel__ oder __Wahrheitstabelle__.
## Konjunktion
Aus zwei Aussagen $p$ und $q$ kann man die Aussage $p∧q$ (gesprochen “p und q”) bilden. Diese zusammengesetzte Aussage ist genau dann wahr, wenn beide Aussagen $p$ und $q$ wahr sind.
## Disjunktion
Dies ist die Verknüpfung zweier Aussagen mit “oder”, als Formel: $p ∨ q$ (gesprochen “p oder q”). Die Aussage $p ∨ q$ ist wahr, wenn $p$ oder $q$ (oder beide) wahr sind, sie ist genau dann falsch, wenn sowohl $p$ als auch $q$ falsch sind.
## Äquivalenz
“Äquivalent” bedeutet “gleichwertig”. Werden zwei Aussagen $p$ und $q$ mit der Äquivalenzverknüpfung zu einer Gesamtaussage zusammengebaut, so ist die Gesamtaussage genau dann wahr, wenn die beiden einzelnen Aussagen $p$ und $q$ den gleichen Wahrheitswert haben. Die so definierte Aussage $p ⇔ q$ (gesprochen “p ist zu q äquivalent.” oder auch “p genau dann, wenn q.”) ist also genau dann wahr, wenn $p$ und $q$ beide wahr oder beide falsch sind.
## Implikation
Hier werden zwei Aussagen $p$ und $q$ zu der Gesamtaussage $p ⇒ q$ (gesprochen “wenn $p$, dann $q$.” oder “$p$ impliziert $q$.”) zusammengefugt. Diese Gesamtaussage soll den Sachverhalt ausdrücken, dass wann immer $p$ wahr ist, auch $q$ wahr sein muss. Man kann sie durch $(¬p) ∨ q$ ausdrucken.
## Tautologie
Eine aussagenlogische Formel, die unabhängig vom Wahrheitswert ihrer Teilformeln immer wahr ist, heißt *allgemeingültig* oder *Tautologie*.
## Satz 1.1.1
- Doppelte Verneinung: $¬(¬p) ⇔ p$.
- De Morgansche Regeln: 
	(a) $¬(p ∨ q) ⇔ (¬p) ∧ (¬q)$
	(b) $¬(p ∧ q) ⇔ (¬p) ∨ (¬q)$
- Distributivgesetze für "und" und "oder":
	(a) $p ∨ (q ∧ r) ⇔ (p ∨ q) ∧ (p ∨ r)$
	(b) $p ∧ (q ∨ r) ⇔ (p ∧ q) ∨ (p ∧ r)$
