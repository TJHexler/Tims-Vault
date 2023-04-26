---
tags: Uni Mathe
---
# 1.2 Quantoren und Prädikatenlogik
Ein Prädikat ist ein Ausdruck, der die Form einer Aussage hat, aber Variablen enthält, zum Beispiel:
	"m ist eine gerade Zahl"
## Quantoren
Eine Aussage wird daraus erst, wenn wir angeben, fur welche m die Aussage gelten soll. Eine Möglichkeit dazu sind Quantoren. 
### Allquantor
Sei M eine Menge, z.B. ein Zahlbereich, und sei $p(m)$ fur jedes Element aus M eine Aussage. Dann können wir mit dem Allquantor die Aussage
	"Für alle $m$ aus $M$ ist die Aussage $p(m)$ wahr."
bilden, mit Formelsymbolen ausgedrückt:
	$\forall m \in M : p(m)$ 
### Existenzquantor
$\exists m \in M:p(m)$
Häufig wird auch der __Quantor der eindeutigen Existenz__ verwendet, dabei wird der Existenzquantor mit einem Ausrufezeichen versehen:
$\exists^! m \in M:p(m)$ bedeutet: "Es existiert __genau ein__ m aus M..."
## Mengen
Eine Menge ist eine wohldefinierte Gesamtheit von Objekten, den Elementen der Menge. Z.B.: Die Menge der natürlichen Zahlen $\mathbb{N} =$ {$1, 2, 3, ...$}
Eine __leere Menge__ ist die Menge, die kein Element enthält. Man schreibt $\emptyset$ oder {}.

Gilt fur zwei Mengen $A$ und $B$, dass jedes Element von $A$ auch ein Element von $B$ ist, so sagt, man $A$ ist eine Teilmenge von $B$, in Zeichen: $A$ ⊆ $B$. Ist $A$ eine Teilmenge von $B$ und ist $A$ nicht gleich $B$, so sagt man, $A$ ist eine echte Teilmenge von $B$, also $A\subset B$.

Fur eine Menge $M$ definieren wir die Potenzmenge von $M$ $Pot(M) :=$ {$A | A ⊆ M$} als die Teilmenge aller Teilmengen von $M$. Eine Potenzmenge einer Menge mit $n$ vielen Elementen hat $2^n$ viele Elemente.

Sind $A$ und $B$ zwei Mengen so definiert man die __Schnittmenge__ $A \cap B$ als die Menge aller Elemente, die in beiden Mengen enthalten sind.
Analog definiert man die __Vereinigung__ $A \cup B$.

Das __kartesische Produkt__ ist die Menge aller geordneten Paare.
$A$ X $B =$ {$(a, b)| a \in A, b \in B$}