---
tags: Uni Mathe
VL-DAte: 10.05.23
---
# Potenzreihen
Durch Potenzreihen können viele Funktionen dargestellt werden
#### Beispiele
- $\sum^{\infty}_{n=0} \frac{z^n}{n!} =: e^z$ Exponentialreihe konvergiert für $z\in\mathbb{C}$
- $\sum^{\infty}_{n=0} \frac{(-1)^n}{(2n+1)!}z^{2n+1} =: sin(z)$
- $\sum^{\infty}_{n=0} \frac{(-1)^n}{(2n)!}z^{2n} =: cos(z)$
Die letzten beiden Reihen konvergieren für alle $z\in\mathbb{C}$.
- $ln(1+x) = \sum^{\infty}_{n=1} \frac{-1^{n-1}}{n}x^n$ konvergiert für $-1<x\leq 1$
- $ln(x) = \sum^{\infty}_{n=1} \frac{-1^{n-1}}{n}(x-1)^n$ konvergiert für $0 < x \leq 2$

## Satz 3.4.8
Es sei $\sum^{\infty}_{n=0} a_n(z-z_0)^n$
1. Es gibt einen eindeutig bestimmten Konvergenzradius $R \in (0, \infty ) \cup \{ \infty \}$, sodass gilt: $\sum^{\infty}_{n=0} a_n(z-z_0)^n = \cases{ist \ absolut \ konvergent \ für |z-z_0| < R \cr ist \ divergent \ für |z-z_0| > R}$
2. Falls $r = \underset{n \rightarrow \infty}{lim} \frac{|a_n|}{|a_{n+1}|}$ oder $r =\underset{n \rightarrow \infty}{lim} \frac{1}{\sqrt[n]{|a_n|}}$ existieren, dann gilt $R=r$
3. Falls $R>0$ und $0 < \delta < R$, dann konvergiert $\sum^{\infty}_{n=0} a_n(z-z_0)^n$ gleichmäßig für $|z-z_0| \leq \delta$. Insbesondere ist die Limesfunktion $z \mapsto \sum^{\infty}_{n=0} a_n(z-z_0)^n$, definiert für alle $z$ mit $|z-z_0| < R$, stetig.
#### Beweis
1. Wir setzen im Beweis $z_0 = 0$. Wir betrachten die Menge $K := \{ |z|: \sum^{\infty}_{n=0} a_nz^n konvergent \}$ wir definieren: $R:= \cases{sup(K) (kleinste obere Schranke) \ falls\ K\ beschränkt \cr \infty falls\ K\ unbeschränkt}$
   1. Fall: Sei $R=0$. Dann ist die Reihe nur für $z=0$ konvergent.
   2. Fall: $R >0$.Wir betrachten ein $z\in\mathbb{C}$ mit $|z| < R$. Es gibt ein $w \in \mathbb{C}$ mit $|z| < |w| < R$ so dass $\sum^{\infty}_{n=0}a_nw^n$ konvergiert. Die Glieder $a_nw^n$ der Reihe sind ab bestimmten Index $n_0$ gleichmäßig beschränkt, d.h. es gibt ein $c \in \mathbb{C}$, sodass $|a_nw^n| \leq C$ für $n \geq n_0$. Wir können mit Hilfe dieses $w$ eine konvergente Majorante für $\sum^{\infty}_{n=0}a_nz^n$ finden. Es ist nämlich $|a_nz^n| = |a_n \frac{w^n}{w^n} z^n| = |a_nw^n|*|\frac{z^n}{w^n}| \leq C*|\frac{z}{w}|^n$ Und da $|\frac{z}{w}| < 1$, ist $\sum^{\infty}_{n=0}C|\frac{z}{w}|^n$ konvergent, also ist das konvergente Mojarante, somit haben wir gezeigt, dass $\sum^{\infty}_{n=0} a_nz^n$ absolut konvergent ist. $\square$
2. Wir wenden das Quotientenkriterium oder Wurzelkriterium auf die Potenzreihe $\sum^{\infty}_{n=0} a_nz^n$ 
   $\underset{n \rightarrow \infty}{lim} |\frac{a_{n+1}z^{n+1}}{a_nz^n}| = \underset{n \rightarrow \infty}{lim} |\frac{a_{n+1}}{a_n}||z| = \frac{1}{r} |z| < 1 \forall |z| < r$ oder $\underset{n \rightarrow \infty}{lim} \sqrt[n]{|a_nz^n|} = |z| \sqrt[n]{|a_n|} = \frac{1}{r} |z| < 1 \forall |z| < r$ 
   Dafür $|z| > r$ Divergenz vorliegt, muss $r=R$ sein
3. Sei $w\in\mathbb{C}$ mit $\delta < |w| < R$. Für $|z| \leq \delta$ gilt die Abschätzung $|a_nz^n| = |a_n \frac{w^n}{w^n} z^n| = |a_nw^n|*|\frac{z^n}{w^n}| \leq C*|\frac{z}{w}|^n$.
   Jetzt folgt die gleichmäßige Konvergenz $\forall z \in \mathbb{C}$, mit $|z| < \delta$ aus dem Weierstrass-Kriterium. $\square$ 
## Bemerkung 3.4.9
Die Formeln für den Konvergenzradius im Satz 3.4.8 funktionieren nur, wenn die entsprechenden Limiten existieren. Es gibt auch eine allgemeinere Formel: Dazu benötigt man den Begriff des __Limes Superior__ = größter Häufungspunkt einer reellen Folge. Man schreibt dafür $\overline{\underset{n \rightarrow \infty}{lim}} a_n$ oder $\underset{n \rightarrow \infty}{lim\ sup} \ a_n$
Falls für eine Potenzreihe gilt: $r= \overline{\underset{n \rightarrow \infty}{lim}} |\frac{a_n}{a_{n+1}}|$ oder $r = \overline{\underset{n \rightarrow \infty}{lim}} \sqrt[n]{|a_n|}$ dann gilt $r=R$

## Anwendungen
- Exponentialreihe
  $e^2= \sum^{\infty}_{n=0} \frac{z^n}{n!}$ Quotientenkriterium $\underset{n \rightarrow \infty}{lim} |\frac{a_n}{a_{n+1}}| = | \frac{(n+1)!}{n!}| = n+1 = \infty$ 
  Dies zeigt: Der Konvergenzradius ist unendlich, die Folge konvergiert für alle $z\in\mathbb{C}$
- Sinus-Reihe
  $sin(z) = \sum^{\infty}_{n=0} \frac{(-1)^n}{(2n+1)!} z^{2n+1}$ Hier gilt, dass die Exponentialreihe eine Konvergente Majorante für alle $z \in \mathbb{C}$ ist. Daher ist $R = \infty$
- ln-Reihe
  Für $ln(1+x) = \sum^{\infty}_{n=0} \frac{(-1)^{n-1}}{n}x^n$ gilt: $\underset{n \rightarrow \infty}{lim} |\frac{a_n}{a_{n+1}}| = \underset{n \rightarrow \infty}{lim} |\frac{n+1}{n}| = 1$
  Der Konvergenzradius ist 1
- Geometrische Reihe
  Für $\sum^{\infty}_{n=0} z^n = \frac{1}{1-z}$ für $|z| < 1$ (geometrische Reihe hier gilt: $a_n = 1 \forall n$) Damit erhalten wir für den Konvergenzradius $\underset{n \rightarrow \infty}{lim} |\frac{a_n}{a_{n+1}}| = \underset{n \rightarrow \infty}{lim} |\frac{1}{1}| = 1$