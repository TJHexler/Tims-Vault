---
tags: Uni Mathe
VL-Date: 05.05.23
---
# 3.4 Funktionenfolgen und -reihen
Wir betrachten heute Folgen $(f_n)_{n\in\mathbb{N}}$ von Funktionen, d.h. für jedes $n\in \mathbb{N}$ ist $f_n: \mathbb{N} \rightarrow \mathbb{N}$ (oder $\mathbb{C}$).

## Definition 3.4.4
Die Folge von Funktion $(f_n)_{n \in\mathbb{N}}$ heißt __punktweise konvergent__, wenn für alle $x \in \mathbb{R}$ gilt, dass die Zahlenfolge $f_n(x)$ konvergent ist.

In diesem Fall können wir eine Limesfunktion $f: \mathbb{R} \rightarrow \mathbb{R}$ durch $f(x) = \underset{n \rightarrow \infty}{lim}f_n(x)$
Die Folge heißt __gleichmäßig konvergent__, wenn gilt: für $\epsilon > 0$ gibt es ein $n_0 \in \mathbb{N}$, so das für alle $n > n_0$ und alle $x \in \mathbb{R}$ gilt: $|f_n(x) - f(x)| < \epsilon$

__punktweise Konvergenz__:
$\forall x \in \mathbb{R} \forall \epsilon > 0 \exists n_0 \in \mathbb{N} \forall n \geq n_0: |f_n(x) - f(x)| < \epsilon$
__gleichmäßige Konvergenz__:
$\forall \epsilon > 0 \exists n_0 \in \mathbb{N} \forall x \in \mathbb{R} \forall n \geq n_0: |f_n(x) - f(x)| < \epsilon$

Kurz gesagt liegt der Unterschied darin, dass es bei der gleichmäßigen Konvergenz eine Schranke $n_0$ für alle x simultan gibt. Gleichmäßige Konvergenz ist eine stärkere Aussage, d.h. aus gleichmäßiger Konvergenz folgt die punktweise Konvergenz, aber nicht umgekehrt.

#### Beispiele
(Hier ersetzen wir den Definitionsbereich $\mathbb{R}$ der Funktionen in der Folge durch das Intervall $D= [-1,+1]$ )
1. Sei $f_n(x) = 1 + \frac{1}{n}x$ Diese Funktionenfolge konvergiert gleichmäßig gegen die Limesfunktion $f: [-1, +1] \rightarrow \mathbb{R}, f(x) = 1$. Denn: Sei $\epsilon > 0$ vorgegeben. Dann ist $|1+\frac{1}{n}x - 1| = |\frac{x}{n}| \leq \frac{1}{n} < \epsilon$ für $n \geq n_0$
2. $f_n(x)=x^{2n}$ Diese Folge konvergiert punktweise auf $[-1, +1]$ gegen $f: f_n(x) = \cases{1, falls\ x = +1 \cr 0, falls\ x \in (-1, +1)}$ Diese Konvergenz ist nicht gleichmäßig konvergent. Wir beobachten, dass die Grenzfunktion (Limesfunktion) nicht stetig ist.

Der nächste Satz sagt, das gleichmäßige Konvergenz die Stetigkeit der Funktion garantiert.

## Satz 3.4.5
Sei $f_n: D \rightarrow \mathbb{R}$ (oder $\mathbb{C}$) eine Folge stetiger Funktionen. Konvergiert $f_n$ gleichmäßig, dann ist der Grenzwert stetig.
#### Beweis
Sei $\epsilon > 0, x_0 \in D$. Wähle $n_0$, so dass $|f_{n_0}(x)-f(x)| < \frac{\epsilon}{3}$ für alle $x \in \mathbb{D}$ gilt. Wähle $\delta > 0$ so, das $|f_{n_0}(x)- f_{n_0}(x_0)| < \frac{\epsilon}{3}$ für alle $x\in D$ mit $|x-x_0|<\delta$
Dann gilt $|f(x)-f(x_0)| \leq |f(x)-f_n(x)| + |f_{n_0}(x)-f_{n_0}(x_0)| + |f_{n_0}(x_0) - f(x_0)|$ falls $|x - x_0| < \delta$ $\square$

## Kriterien für gleichmäßige Konvergenz
#### 1. Cauchy-Kriterium
Falls es zu jedem $\epsilon > 0$ einen Index $n_0$ gibt, so dass für alle $x \in D$ gilt: $|f_n(x) - f_m(x)| < \epsilon$ für alle $n, m \geq n_0$.
Dann ist die Folge gleichmäßig konvergent.
#### 2. Weierstraß-Kriterium
Falls gilt, für eine Reihe $\sum_{n = 0}^{\infty}f_n$ von Funktionen $|f_(x)| < c_n$ für alle $x \in D$ und $\sum_{n = 0}{\infty}c_n$ konvergiert, dann konvergieren $\sum_{n = 0}^{\infty}f_n$ und $\sum_{n = 0}^{\infty}|f_n|$ gleichmäßig.
##### Beispiel
Sei $D = \{ z \in \mathbb{C} | |z| < 1 \}$. Die Reihe $\sum_{n = 0}^{\infty}z^n$ ist auf D punktweise konvergent (geometrische Reihe!) aber nicht gleichmäßig konvergent. Betrachten wir die Folgen der Partialsummen $s_n(z) = \sum_{n = 0}^{\infty}z^n$ und wählen $\epsilon = \frac{1}{z}$, dann gibt es zu jedem $n \in \mathbb{N}$ ein $z \in D$, so dass $| s_{n + 1} - s_n | = |z^{n + 1}| \geq \frac{1}{2}$ (vgl. Bsp. 2 oben).

# Potenzreihen
Potenzreihen sind ein wichtiges Hilfsmittel in der Mathematik, um Funktionen darzustellen.
## Definition 3.4.7
Sei $z_0 \in \mathbb{C}$ und sei $(a_k)_{n \in \mathbb{N}}$ eine Folge komplexer Zahlen. Dann heißt $\sum_{k = 0}^{\infty}a_k(z - z_0)^k$ eine Potenzreihe um (den Entwicklungspunkt) $z_0$ mit Koeffizienten $a_k$. Sie ist für alle $z \in \mathbb{C}$ definiert, für die die Reihe konvergiert (Falls $z, z_0, a_k \in \mathbb{R}$, dann heißt die Reihe __reell__).
Falls $z_0 = 0$, dann hat die Reihe die Form $\sum_{k = 0}^{\infty}a_kz^k$ (Entwicklung um Null).
##### Beispiele
1. Die Exponentialreihe $\sum_{k = 0}^{\infty} \frac{z^k}{n} = exp(z) e^z$ konvergent für alle $z \in \mathbb{C}$
2. $\sum_{k = 0}^{\infty} \frac{(-1)^n}{(2n + 1)!}z^{2n+1} = sin(z)$ 