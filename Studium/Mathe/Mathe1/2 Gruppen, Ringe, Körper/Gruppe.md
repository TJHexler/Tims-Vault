---
tags: Uni Mathe
---
# 2.1 Gruppen
## Definition 2.1.1 Gruppenaxiome

Sei $G$ eine Menge mit einer Verknüpfung $\star: G \times G \rightarrow G, (a, b) \rightarrow a*b$. Die Menge $G$, zusammen mit der Verknüpfung $\star$ heißt __Gruppe__, wenn die folgenden drei Eigenschaften gelten:
- __Assoziativität__: $(a*b)*c = a*(a*b)$
- Es gibt ein __neutrales Element__: $\exists e \in G \forall a \in G: a*e =e*a = a$ 
- Es gibt zu jedem Element ein __inverses Element__: $\forall a \in G \exists b \in G:a*b=b*a=e$
Hat die Verknüpfung $\star$ zusätzlich die Eigenschaft der __Kommutativität__
- $\forall a, b \in G: a*b = b*a$
so wird die Gruppe G eine __abelsche (oder kommutative) Gruppe__ genannt.

#### Beweis: Es kann nur ein neutrales Element geben
Sei $f \in G$ ein Element mit der Eigenschaft, das $f*a=a$ für alle $a\in G$ gilt. Dann folgt $e = f *e = f$.
Außerdem gilt fur jedes $a \in G$, dass das inverse Element zu a eindeutig bestimmt ist. Deshalb darf man $a^{-1}$ für das eindeutig bestimmte inverse Element zu  $a$ schreiben. Dies zeigt man wie folgt: 
Seien $b, c \in G$ mit $b*a =e$ und $a*c=e$. Daraus schließen wir 
$b=b*e=b*(a*c)=(b*a)*c=e*c=c$

## Definition 2.1.2
Sei $G$ eine Gruppe. Eine nichtleere Teilmenge $H \subseteq G$ wird als __Untergruppe__ von $G$ bezeichnet, falls die folgenden beiden Eigenschaften gelten:
- Die Teilmenge $H$ ist abgeschlossen unter der Gruppenverknüpfung: $\forall a, b \in G: a*b\in G$
- Die Teilmenge $H$ ist abgeschlossen unter der Inversenbildung: $\forall a \in H: a^{-1}\in H$

Es folgt sofort aus diesen beiden Eigenschaften, dass jede Untergruppe von G das neutrale Element von G enthalt, denn eine nichtleere Teilmenge H ⊆ G enthält mindestens ein Element a ∈ H und nach (UG2) somit auch $a^{-1}$. Dann folgt aber mit (UG1), dass $a ∗ a^{-1} = e$ in $H$ liegt.

Für jede Gruppe ist $\{ e \}$ eine Untergruppe, die __triviale Untergruppe__.

## Definition 2.1.3 Gruppenhomomorphismus
Seien $G, H$ zwei Gruppen. Eine [[Abbildung]] $f: G \rightarrow H$ heißt __Gruppenhomomorphismus__, wenn $f(ab) = f(a)f(b)$ für alle $a, b \in G$ gilt.

## Definition 2.1.4 Kern
Sei $f: G \rightarrow H$ ein Gruppenhomomorphismus und sei $e \in H$ das neutrale Element. Dann heißt $ker(f):= f^{-1}(\{ e \} ) = \{ g \in G | f(g) = e \}$ der Kern von f.

## Satz 2.1.6
Sei $f: G \rightarrow H$ ein Gruppenhomomorphismus. Dann bildet $f$ das neutrale Element von $G$ auf das neutrale Element von $H$ ab. Außerdem sind $ker(f)$ und $Bild(f)$ Untergruppen von $G$ bzw. $H$.