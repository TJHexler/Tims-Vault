---
tags: Uni Mathe
---
# 1.5 Abbildungen
Seien $A$ und $B$ Mengen und sei $F ⊆ A × B$ eine [[Relation]]. Die [[Relation]] $F$ heißt Abbildung oder Funktion von $A$ nach $B$, wenn gilt $∀x ∈ A ∃^! y ∈ B : (x, y) ∈ F$.

Eine Abbildung kann man sich auch als eine Zuordnungsvorschrift denken, die jedem Element $a$ von $A$ ein eindeutig bestimmtes Element von $B$ zuordnet. Daher schreiben wir $F : A → B$ und bezeichnen das eindeutig bestimmte Element aus $B$, das mit $x ∈ A$ in [[Relation]] steht, mit $F(x)$. Das Element $F(x)$ nennen wir auch den Wert von $F$ bei $x$ oder das Bild des Elements $x$. Gilt $y = F(x)$, so sagen wir auch, $x$ wird auf $y$ abgebildet und schreiben dafür $x→ y$. 

Ein Element $x ∈ A$ mit $F(x) = y$ bezeichnet man auch als ein __Urbild__ von $y$. Die Menge $A$ heißt __Definitionsbereich__, die Menge $B$ __Bildbereich__ oder __Wertebereich__ von $F$.
## Bild einer Abbildung
Für eine Abbildung $F : A → B$ heißt $Bild(F) := \{ y ∈ B | ∃x ∈ A: F(x) = y\}$ das __Bild__ der Abbildung $F$. Gilt $Bild(F) = B$, stimmt also das Bild mit dem Bildbereich überein, dann nennt man die Abbildung $F$ __surjektiv__.

## Injektiv, Surjektiv, Bijektiv
Eine Abbildung $F : A → B$ ist genau dann __surjektiv__, wenn jedes $y ∈ B$ mindestens ein Urbild besitzt. 
Für eine Teilmenge $M ⊆ A$ nennt man $F(M) := \{ y ∈ B | ∃x ∈ M : F(x) = y\}$ das Bild der Teilmenge $M$. Es gilt $Bild(F) = F(A)$. Für eine Teilmenge $N ⊆ B$ nennt man $F^{-1} (N) := \{ x ∈ A | F(x) ∈ N\}$ das __Urbild__ der Teilmenge $N$. Es gilt $F^{-1} (B) = A$.
Gilt für jede einelementige Teilmenge $\{ y\}$ von $B$, dass das Urbild $F^{-1} (y)$ aus höchstens einem Element besteht, so heißt die Abbildung __injektiv__.

Eine Abbildung heißt __bijektiv__, wenn sie sowohl injektiv aus auch surjektiv ist.
Genau dann, wenn eine Abbildung $F : A → B$ bijektiv ist, gibt es dazu eine Umkehrabbildung, d.h. eine Abbildung $G: B → A$, so dass $G(F(a)) = a$ für alle $a ∈ A$ und $F(G(b)) = b$ für alle $b ∈ B$ gilt, wie man sich leicht überlegt. Wenn eine Umkehrabbildung existiert, ist sie eindeutig bestimmt.

## Mächtigkeit
Bei einer endlichen Menge nennt man die Anzahl der Elemente die Mächtigkeit der Menge. Allgemeiner nennt man zwei Mengen gleichmächtig, wenn es eine bijektive Abbildung zwischen ihnen gibt. Gibt es eine surjektive Abbildung $M → N$ zwischen zwei Mengen, so sagt man, dass die Mächtigkeit$ von $M$ großer gleich der Mächtigkeit von $N$ ist.

## Die identische Abbildung
Ist $X$ eine Menge so bezeichnen wir mit $id_X$ die *identische Abbildung* $id_X: X \rightarrow X, x \rightarrow x$, die jedes Element von $X$ wieder auf sich selbst abbildet.

## verkettete Abbildungen
Sind $F : A → B$ und $G: B → C$ zwei Abbildungen, so ist durch $G ◦ F : A → C, a → G(F(a))$, die Verkettung von F mit G definiert.

Sind zwei Abbildungen gegeben, die eine Menge in sich abbilden, so erhalt man im Allgemeinen verschiedene Abbildungen, je nachdem, in welcher Reihenfolge man verkettet: Seien die beiden Funktionen $f, g : R → R$ definiert durch $f(x) = x^2 , g(x) = x + 1$. Dann gilt $(f ◦ g)(x) = x^2 + 2x + 1$, aber $(g ◦ f)(x) = x^2 + 1$.

Die Verkettung von Abbildungen ist jedoch __assoziativ__: Sind $F : A → B, G: B → C$ und $H : C → D$ drei Abbildungen, dann gilt: $(H ◦ G) ◦ F = H ◦ (G ◦ F)$.

## Einschränkungen
Ist $f : M → N$ eine Abbildung und $A ⊆ M$ eine Teilmenge, dann definiert $f|_A : A → N, f|_A(a) := f(a)$ eine Abbildung von $A$ nach $N$, diese Abbildung wird die Einschränkung der Abbildung $f$ auf $A$ genannt. Es gilt, dass die Einschränkung einer injektiven Abbildung stets injektiv ist.