---
tags: Uni Mathe
VL-Date: 21.04.23
---
# 3.2 Zahlenfolgen und Zahlenreihen
Hier: $X = \mathbb{R},\mathbb{C}$
## Rechnen mit Grenzwerten
### Satz 3.10
Seien $(x_n)_{n\in\mathbb{N}}$ und $X $(y_n)_{n\in\mathbb{N}}$ zwei konvergente Folgen in $\mathbb{R}$ mit $\underset{n\rightarrow\infty}{lim} x_n = x, \underset{n\rightarrow\infty}{lim} = y, x_n <= y_n$ 
Dann gilt: $x <= y$
#### Beweis
Angenommen, $x > y$. Sei $\epsilon = x - y$. Dann gibt es ein $n_0 \in\mathbb{N}$, sodass $|y_n-y|<\epsilon$ und es gibt ein $m_0 \in \mathbb{N}$, sodass $|x_n - x|<\epsilon$. Dann gilt für ein $k >= max(n_0, m_0)$
Dann gilt $|x_k-x|<\epsilon$ und $|y_n-y|<\epsilon$.
Widerspruch gezeigt: Für konvergente Foglen gilt: $x_n<=y_n \Rightarrow \underset{n\rightarrow\infty}{lim} x_n <= \underset{n\rightarrow\infty}{lim} y_n$ 
Aber: Es gilt __nicht__ $x_n<y_n$, sodass $\underset{n\rightarrow\infty}{lim} x_n < \underset{n\rightarrow\infty}{lim} y_n$, denn z.B. $\frac{-1}{n} \rightarrow 0$ und $\frac{1}{n} \rightarrow 0$ 
### Bemerkung 3.11
Eine Folge $x$ heißt __beschränkt__, falls es ein $C\in \mathbb{R}$ und ein $x_0 \in X$, sodass $x_n \in K_C(x_0)$ für alle $n \in \mathbb{N}$
Konvergente Folgen sind immer beschränkt, denn:
nur endlich viele liegen außerhalb einer Kugelumgleichung $K_\epsilon(x)$, wenn $x_n \rightarrow x$

Wähle dann $C:= max(\gamma(x_1,x),..., \gamma(x_{n_0-1}), \epsilon)$ falls $x_n \in K_{\epsilon}(x)$ liegen für $n >= n_0$
Nicht alle beschränkten Folgen konvergieren, z.B. $(-1)^n$ konvergiert nicht.

### Satz 3.12
Seien  $(x_n)_{n\in\mathbb{N}}$ und  $(y_n)_{n\in\mathbb{N}}$ konvergente reelle (oder komplexe) Folgen und $\alpha, \beta$ reelle (oder komplexe). Dann gilt:
- $|\underset{n\rightarrow\infty}{lim} x_n| = \underset{n\rightarrow\infty}{lim} |x_n|$
- $\underset{n\rightarrow\infty}{lim} a*x_n=a*\underset{n\rightarrow\infty}{lim} x_n$
- $\underset{n\rightarrow\infty}{lim} (x_n \pm y_n) = \underset{n\rightarrow\infty}{lim} x_n \pm \underset{n\rightarrow\infty}{lim} y_n$
-  $\underset{n\rightarrow\infty}{lim} (x_n * y_n) = \underset{n\rightarrow\infty}{lim} x_n * \underset{n\rightarrow\infty}{lim} y_n$
- falls $x_n >= 0$: $\underset{n\rightarrow\infty}{lim} \sqrt{x_n} = \sqrt{\underset{n\rightarrow\infty}{lim} x_n}$
- falls $y_n != 0$ und $\underset{n\rightarrow\infty}{lim} y_n != 0$, dann gilt: $\underset{n\rightarrow\infty}{lim} \frac{x_n}{y_n}= \frac{\underset{n\rightarrow\infty}{lim} x_n}{\underset{n\rightarrow\infty}{lim} y_n}$
#### Beweis
Nur die Regel für die Multiplikation: Sei $x=\underset{n\rightarrow\infty}{lim} x_n, y = \underset{n\rightarrow\infty}{lim} y_n$
Es gilt:
$|x_ny_n-xy| =$
$=\frac{1}{2}|(x_n+x)(y_n-y)+(y_n+y)(x_n-x)|$
$<=\frac{1}{2}(|x_n+x||y_n-y|+|y_n+y||x_n-x|)$
Erster und dritter Betrag $<M$, zweiter und vierter $=\epsilon$
$<M\epsilon$, wobei wir benutzt haben, dass konvergente Folgen beschränkt sind. $\square$ 

## Konvergenzkriterium
### Satz 3.13 Einschließungskriterium
Seien  $(x_n)_{n\in\mathbb{N}}$ und $X $(y_n)_{n\in\mathbb{N}}$ und $(z_n)_{n\in\mathbb{N}}$ reelle Zahlenfolgen und $x_n <= z_n <= y_n$ und $\underset{n\rightarrow\infty}{lim} x_n = x = \underset{n\rightarrow\infty}{lim} y_n$
Dann konvergiert $z_n$ gegen $x$
#### Beweis
Sei $\epsilon > 0$.
$|x-z_n|=\cases{z_n - x <= y_n -x <= |y_n -x| < \epsilon:für |z_n >= x}{x-z_n <= x-x_n <= |x-x_n| < \epsilon: falls z_n < x}$ für $n$ genügend groß. $\square$

### Definition 3.16
Die Folge $(x_n)_{n\in\mathbb{N}}, x_n \in \mathbb{R}$ heißt:
- __streng monoton wachsend__, falls $x_{n+1}>x_n$
- __streng monoton fallend__, falls $x_{n+1}<x_n$
- __monoton steigend__, falls $x_{n+1}>=x_n$
- __monoton fallend__, falls $x_{n+1}<=x_n$
für alle $n\in \mathbb{N}$.

### Satz 3.17
Beschränkte, monoton wachsende (bzw. fallende) Folgen sind konvergent.
#### Beweis
Sei $x_n <= x_{n+1} <= c$
Dann existiert eine kleinste obere Schranke, ein sogenanntes __Supremum__, für die Menge $\{x_n|n \in \mathbb{N}\}$ der Folgenmitglieder. Dies folgt aus der Vollständigkeit der reellen Zahlen.
Setze dieses $c_{min}= sup\{x_n|n\in \mathbb{N}\}$ als die kleinste obere Schranke. Dann gilt:
Zu jedem $\epsilon > 0$ existiert ein $n_0\in \mathbb{N}$, sodass $c_{min}-\epsilon < x_{n_0}$ 
Aber die Folge ist monoton wachsend, also liegen auch alle weiteren Folgenglieder $x_n$ mit $n>=n_0$ zwischen $c_{min}$ und $c_{min} - \epsilon$ Dies zeigt, dass $x_n \rightarrow c_{min}$ geht . $\square$

### Definition 3.18
Sei $(x_n)_{n\in\mathbb{N}}$ eine Folge reeller oder komplexen Zahlen und $\mathbb{N}^{'} \subset \mathbb{N}$ eine unendliche Teilmenge. Dann heißt  $(x_n)_{n\in\mathbb{N}^{'}}$ eine __Teilfolge__ von  $(x_n)_{n\in\mathbb{N}}$
#### Alternative Definition
Sei  $(x_n)_{n\in\mathbb{N}}$ eine Folge und $(n_k)_{k\in \mathbb{N}}$ eine streng monoton wachsende Folge von natürlichen Zahlen. Dann ist $(x_n)_{n\in\mathbb{N}}$ eine Teilfolge 
z.B. hat die divergente Folge $(x_n)_{n\in\mathbb{N}}, x_n = (-1)^n$ die konvergente (sogar konstante) Teilfolge $(x_{2k})_{k \in \mathbb{N}}, x_{2k} = (-1)^{2k} = +1$ 

### Definition 3.19
Ein Element $a\in \mathbb{R}$ oder $\mathbb{C}$ heißt __Häufungspunkt__ der Folge $(x_n)_{n\in\mathbb{N}}$, falls es eine gegen a konvergente Teilfolge gibt.
z.B. sind $+1$ und $-1$ Häufungspunkte der Folgen $x_n = (-1)^n$ und $y_n = (-1)^n+\frac{1}{n}$ 