---
tags: Uni Mathe
VL-Date: 19.04.23
---
# Analysis [[Grundbegriffe]]
Sändig Skript ab Seite 149.
Analysis ist die Differential- und Integralrechnung, alternativ ...
## zentrale Begriffe
- Grenzwert
- Stetigkeit
- Differenzierbarkeit
- Integrale
Wir betrachten diese Begriffe auch in höher-dimensionalen Räumen.
# 3.1 Konvergenz in metrischen Räumen
Konvergenz bedeutet Annäherung an einen Wert, um die Güte der Annäherung bestimmen zu können, benötigt man eine Abstandsschrift.
## Definition 3.1 Metrik, metrische Räume
Sei $X$ eine Menge. Eine [[Abbildung]] $\gamma : X \chi X \rightarrow R, (x,y) \rightarrow  \gamma (x,y)$ heißt __Metrik__ oder __Abstandsfunktion__, wenn sie folgende Eigenschaften für alle $x,y,z  \in X$ besitzt:
- (M1) $\gamma (x,y) >= 0$ und es gibt $\gamma (x,y) = 0$ genau dann, wenn $x = y$
- (M2) $\gamma (x,y) = \gamma (y,x)$ __symmetrisch__
- (M3) $\gamma (x,z) <= \gamma (x,y) + \gamma (y,z)$ __Dreiecksgleichung__

Die Menge $X$, versehen mit solch einer Metrik heißt __metrischer Raum__.
### Beispiele
0. $\gamma (x,y) = |x-y|$ ist eine Abstandsfunktion auf $\mathbb{R}$ (und $\mathbb{C}$)
1. Im $\mathbb{R}^n$ kann man den __Euklidischen Abstand__ $|| x-y || = \sqrt{\langle x-y, x-y\rangle}$ (unter der Wurzel ist das sogenannte Skalarprodukt)
2. Bei rechtwinkligem Straßennetz: $\gamma:\mathbb{R}^n\times\mathbb{R}, \gamma(x,y)=|x_1-y_1|+...+|x_n-y_n|$ 
3. Maximum-Metrik auf $\mathbb{R}^n : \gamma (x,y) := max\{ |x_1 - x_1|, ..., |x_n - y_n|\}$
4. Die diskrete Metrik: $d(x,y) = 0$ falls $x = y, 1$ sonst
5. Hammingabstand: Anzahl an Stellen, an denen sich zwei Binärzahlen unterscheiden

### Annahme 
Wenn nichts anderes gesagt wird, nehmen wir an, das $\mathbb{R}^n, \mathbb{R}$ und $\mathbb{C}$ mit der Abstandsfunktion 0) bzw. 1) versehen sind.

## Definition 3.2
Sei $X$ ein metrischer Raum und $x_0 \in X$ und $\epsilon > 0$ eine reelle Zahl. Unter einer __Kugelumgebung__ mit Radius $\epsilon$ und Mittelpunkt $x_0$ verstehen wir die Menge $K_{\epsilon} (x_0) := \{ x \in X | \gamma(x, x_0) < \epsilon\}$ 

## Definition 3.3
Sei $X$ ein metrischer Raum. Eine Teilmenge $U \subseteq X$ heißt __offen__, wenn zu jedem $x_0  \in U$ eine Kugelumgebung von $x_0$ existiert, die ganz in $U$ liegt.
Eine Teilmenge $A \subseteq X$ heißt __abgeschlossen__, falls das Komplement offen ist.

## Definition 3.4
Sei $X$ eine Menge. Eine __[[Folge]]__ ist eine [[Abbildung]] $\mathbb{N} \rightarrow X$ so dass jede natürliche Zahl $n$ ein $a_n \in X$ zugewiesen wird. Wir schreiben $(a_n)_{n \in \mathbb{N} } =a_n$ für die [[Folge]].
Die Elemente $a_n \in X$ heißen __Folgenglieder__

## Definition 3.5
Die [[Folge]] in dem metrischen Raum $X$ __konvergiert__ gegen das Element $a \in X$, falls folgendes gilt: $\forall \epsilon > 0 \exists n_0 \in \mathbb{N} \forall n >= n_0: \gamma (a_n, a) < \epsilon$ 
Anders formuliert: $(a_n)_{n \in \mathbb{N} }$ konvergiert gegen $a$, in Zeichen $a_n \rightarrow  a$, falls für jede Kugelumgebung von $a$ gilt, dass höchstens endlich viele Folgenglieder $a_n$ in der Kugelumgebung enthalten sind.

Falls eine der obigen äquivalenten Bedingungen gilt, dann nennt man $a$ den __Grenzwert__ oder __Limes__ von $(a_n)_{n \in \mathbb{N} }$ und man schreibt $\underset{n \rightarrow \infty}{lim} a_n = a$ 
Falls $(a_n)_{n \in \mathbb{N} }$ nicht gegen ein Element $a \in X$ konvergiert, sagt man $(a_n)_{n \in \mathbb{N} }$ ist __divergent__.
### Beispiele
- $a_n = \frac{1}{n}$ in $\mathbb{R}$ konvergiert gegen 0 (Nullfolge)
- $a_n = n$ ist divergent ($a_n \rightarrow +\infty$ "bestimmte Divergenz")
- $a_n = (-1)^n$ ist (unbestimmt) divergent
- $a_n = (-n)^n$ ist divergent
- konstante Folgen sind konvergent

## Hilfssatz 3.7
Der Grenzwert einer konvergenten [[Folge]] ist eindeutig bestimmt in einem metrischen Raum
(Beweis siehe Skript)

## Bemerkung
Dass man in einen metrischen Raum von zwei verschiedenen Punkte disjunkte Kugelumgebungen findet, nennt man dies Hausdorfeigenschaft von metrischen Räumen.