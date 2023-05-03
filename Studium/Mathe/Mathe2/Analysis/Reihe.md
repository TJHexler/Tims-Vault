---
tags: Uni Mathe
VL-Date: 26.04.23
---
# Reihen
## Satz 3.20 Cauchysches Konvergenzkriterium
Eine [[Folge]] reeller oder komplexer Zahlen $(x_n)_{n  \in \mathbb{N}}$ konvergiert genau dann, wenn sie eine __Cauchy-Folge__ ist, d.h. für alle $\epsilon > 0$ gibt es ein $n0$, so dass für alle $n, m >= n_0$ gilt: $|x_n - x_m| < \epsilon$
Vorteil des Cauchykriteriums: Konvergenz einer Folge beweisen, ohne Limes

## Bemerkung
Cauchy-Folgen kann man allgemein in metrischen Räumen analog definieren. Ein metrischer Raum heißt __vollständig__, wenn jede Cauchy-Folge konvergiert.

## Definition 3.22
Sei $(x_n)_{n  \in \mathbb{N}}$ eine [[Folge]] in $\mathbb{R}$ (oder $\mathbb{C}$). Der Ausdruck $\sum^{\infty}_{k = 1} a_k$ heißt (unendliche) __Reihe__, $a_k$  heißen die __Glieder__ der Reihe. Unter einer __Partialsumme__ versteht man eine endliche Summe $s_n = a_1 + a_2 + ... +a_n = \sum^{n}_{k=1} a_k$ 
Konvergiert die Folge der Partialsummen $(s_n)_{n  \in \mathbb{N}}$ gegen einen Grenzwert $s$ in $\mathbb{R}$ (oder $\mathbb{C}$), dann sagt man, $\sum^{\infty}_{k = 1} a_k$ konvergiert und schreibt $\underset{n \rightarrow \infty}{lim} s_n = s =: \sum^{\infty}_{k = 1} a_k$ 
$\underset{n \rightarrow \infty}{lim} \sum^{\infty}_{k = 1} a_k$

Besitzt $(s_n)_{n  \in \mathbb{N}}$ keinen Grenzwert, so spricht man von einer divergenten Reihe.

### Beispiele
#### Teleskopsumme
#### Geometrische Reihe
$\sum^{\infty}_{k = 0} q^k = 1 + q + q^2 + q^3 + ...$
Konvergiert gegen $\frac{1}{n-q}$ falls $|q| < 1$, divergent sonst
#### harmonische Reihe
$\sum^{\infty}_{k = 1} \frac{1}{k} = 1 + \frac{1}{2} + ...$ ist divergent.

## Satz 3.24
Die Reihe $\sum^{\infty}_{k = 1} a_k$ sei divergent. Dann gilt: Die [[Folge]] $(a_k)_{n \in \mathbb{N}}$ ist eine __Nullfolge__, d.h. konvergiert gegen __Null__.
#### Beweis
Aus dem Cauchy-Kriterium, angewandt auf die Folge der Partialsummen $s_n$ folgt insbesondere, das es 
ein $n_0 \in \mathbb{N}$ gibt, so dass $|s_{m + 1} - s_m| < \epsilon$ für alle $m \geq n_0$. Es gilt aber: $s_{m + 1} - s_m = a_{m + 1}$, was zeigt, das $a_k$ eine Nullfolge ist. $\square$ 

## Hilfssatz 3.26
Eine Reihe mit nicht negativen Gliedern, für die die [[Folge]] der Partialsummen beschränkt ist, ist konvergent.
#### Beweis
Da $a_k \geq 0$, gilt $s_n$ ist monoton wachsend, aber folgt der Behauptung aus Satz 3.17 (monoton und beschränkte Folgen sind konvergent). $\square$

## Definition 3.27
Eine Reihe heißt alternierend, wenn die Folge $(a_k)$ wechselnde Vorzeichen besitzt.

## Satz 3.28 Leibniz-Kriterium
Sei $(a_k)_{k \in \mathbb{N}}$ eine reelle Folge, für die gilt: $a_k \geq 0, a_k \geq a_{k + 1}$ und $\underset{k \rightarrow \infty}{lim} a_k = 0$. Dann ist die __alternierende Reihe__ $\sum^{\infty}{k= 0} (-1)^ka_k$ konvergent.
#### Beweis
Siehe [[Saendig_Mathe fuer inf swt I.pdf]] Seite 164.

#### Beispiel
Die alternierende harmonische Reihe $\sum^{\infty}_{k = 1} (-1)^{k-1} \frac{1}{k}$ 
Des weiteren gilt: $\sum^{\infty}_{k = 1} (-1)^{k-1} \frac{1}{k} = ln 2$

## Bemerkung 1
Umordnung in Reihe $\sum^{\infty}_{k = 1} (-1)^{k-1} \frac{1}{k}$. Wir ordnen die Folgenglieder nun so um, sodass eine positive Summe entsteht. Da für gerades $m$ gilt: $\frac{1}{m+1}+\frac{1}{m+3}+...+\frac{1}{2m-1} \geq \frac{m}{2} * \frac{1}{2m} = \frac{1}{4}$, wird die umgeordnete Reihe divergent sein.

## Bemerkung 2
$(1 − 1) + (1 − 1) + · · · = 0$ und $1 + (−1 + 1) + (−1 + 1) + · · · = 1$ 
Die Klammerungen führen zu unterschiedlichen Ergebnissen. Um Umordnen zu können, braucht man stärkere Eigenschaften.