---
tags: Uni Mathe
VL-Date: 28.04.23
---
# Absolute Konvergenz
Haben bereits für eine [[Reihe]] gesehen, dass bei Umordnung das Konvergenzverhalten der Reihe ändern kann.
Ähnlich: Für endliche Summen gilt auch **kein Assoziativgesetz**:
- $\sum^\infty_{k=0} (-1)^k = 1-1+1-1+... \overset{?}{=} \cases{(1-1)+(1-1)+...= 0 \cr 1+(-1+1)+(-1+1)+...=1}$ 
Um eine Reihe ohne Veränderung des Konvergenzverhaltens umordnen zu können, benötigt man einen stärkeren Begriff von Konvergenz.

## Definition 3.29
Eine reelle/komplexe Zahlenreihe $\sum^\infty_{k=1} a_k$ heißt **absolut konvergent**, falls $\sum^\infty_{k=1} |a_k|$ konvergiert

## Satz 3.30
Jede absolut konvergente Reihe ist konvergent.
#### Beweis
Verwenden Cauchy-Kriterium:
- Für jedes $\varepsilon > 0$ gibt es ein $n_0$ für das gilt:
- $|s_m-s_n| = |\sum^m_{k=n+1} a_k| \leq \sum_{k=n+1}^m |a_k| < \varepsilon$ 
Umkehrung gilt nicht:
- Denn $\sum^\infty_{k=1} (-1)^k a_k$ konvergiert, aber $\sum^\infty_{k=1} \frac{1}{k}$ divergiert.

# Majo-, Minoranten-, Wurzel- und Quotientenkriterium
## Satz 3.32 (Majorantenkriterium)
Seien $(a_k)_{k \in \mathbb{N}}$ und $(b_k)_{k \in \mathbb{N}}$ Folgen mit $|a_k| \leq b_k$ 
Ist $\sum_{k=1}^\infty b_k$ konvergent, dann ist $\sum^\infty_{k=1} |a_k|$ konvergent (und somit auch $\sum^\infty_{k=1} a_k$)
In diesem Fall nennt man $\sum^\infty_{k=1} b_k$ eine **konvergente Majorante** von $\sum^\infty_{k=1} |a_k|$ bzw. $\sum^\infty_{k=1} a_k$
#### Beweis
Mit Cauchy-Kriterium:
- Sei $s_n := \sum^\infty_{k=1} |a_k|$. Dann gibt es zu jedem $\varepsilon>0$ ein $n_0 \in \mathbb{N}$, so dass für alle $m \geq n \geq n_0$ gilt:
- $|s_m - s_n| = \sum^m_{k=n+1} |a_k| = \sum^m_{k=n+1} b_k = |\tilde{s}_m - \tilde{s}_n| < \varepsilon$ wobei $\tilde{s}_n = \sum^n_{k=1} b_k$ ist.
- Damit ist gezeigt, dass $s_n$ eine Cauchy-Folge ist.

Es gibt auch ein **Minorantenkriterium**, dass direkt aus dem Satz folgt:
- Sei $a_k \geq c_k \geq 0$ und sei $\sum^\infty_{k=1} c_k$ divergent.
- Dann divergiert auch $\sum^\infty_{k=1} a_k$ 

#### Beispiel
1. $\sum^\infty_{k=1} \frac{1}{n^2}$ 
	- Da $\frac{1}{n^2} \leq \frac{1}{n(n-1)}$ für $n \geq 2$ und $\sum^\infty_{n=2} \frac{1}{n(n-1)} = 1$, haben wir eine konvergente Majorante gefunden, also konvergiert $\sum^\infty_{n=1} \frac{1}{n^2}$ 
2. $\sum^\infty_{k=1} \frac{1}{\sqrt{n}}$ 
	- Minorantenkriterium, da $\frac{1}{n^2} \geq \frac{1}{n}$ und $\sum^\infty_{k=1} \frac{1}{n}$ divergiert
	- Also divergiert $\sum^\infty_{k=1} \frac{1}{\sqrt{n}}$
3. $\sum^\infty_{n=1} \frac{1}{2^n+3^n}$
	- Da $\frac{1}{2^n+3^n} \leq \frac{1}{3^n} = (\frac{1}{3})^n$ ist $\sum^\infty_{n=1} (\frac{1}{3})^n$ die geometrische Reihe eine konvergente Majorante.

## Satz 3.33 (Wurzelkriterium)
Die Reihe $\sum^\infty_{k=1} a_k$ ist absolut konvergent, falls es ein $q$ mit $0\leq q < 1$ gibt und ein $k_0 \in \mathbb{N}$ existiert, so dass $\sqrt[k]{|a_k|} \leq q$ für alle $k \geq k_0$ gilt.
#### Beweis
Es gilt $|a_k| \leq q^k$ und $\sum^\infty_{k=0} q^k$konvergiert für $q<1$ (geometrische Reihe)

## Satz 3.34 (Quotientenkriterium)
Sei $a_k \neq 0$ für $k \geq k_0$ 
Die Reihe $\sum^\infty_{k=1} a_k$ ist absolut konvergent, falls es ein $q$ mit $0\leq q < 1$ gibt, so dass $|\frac{a_{k+1}}{a_k}| \leq q$ gilt für alle $k \geq k_0$ gilt.

#### Beweis
Aus $|\frac{a_{k+1}}{a_k}| \leq q$ folgt $|a_{k+1}| \leq q |a_k| \leq q^2 |a_{k-1}| \leq ... \leq q^{k+1-k_0} |a_{k_0}|$.
Daher ist $\sum^\infty_{k=k_0} |a_k| \leq \frac{|a_k|}{q^k} \sum^\infty_{k=k_0} q^k$ und wir haben eine konvergente Majorante gefunden.

#### Beispiele
- **Exponentialreihe** $\sum^\infty_{k=0} \frac{x^k}{k!}$ wobei $x \in \mathbb{R}$. Es ist nach dem Quotientenkriterium $\underset{k\rightarrow \infty}{lim}|\frac{x^{k+1} \cdot k!}{(k+1)! \cdot x^k}| = \underset{k\rightarrow \infty}{lim} \frac{x}{k+1} = 0$. Also konvergiert die Reihe.
- **harmonische Reihe** $\sum^{\infty}_{k=1} \frac{1}{k}$. Das Quotientenkriterium liefert: $|\frac{a_{k+1}}{a_k}| = \frac{k}{k + 1} < 1$, aber es gilt nicht $\frac{k}{k+1} \leq q < 1$ für alle $k \geq k_0$, da $\underset{k \rightarrow \infty}{lim} |\frac{a_{k + 1}}{a_k}| = 1$ ist. Somit ist die harmonische Reihe divergent. Das Wurzelkriterium führt ebenfalls auf $\underset{k \rightarrow \infty}{lim} \sqrt[k]{\frac{1}{k}} = 1$.

### Bemerkungen

- Falls $\sqrt[k]{|a_k|} \geq 1$ , dann ist $\sum^\infty_{k=0} a_k$ divergent
- Falls $|\frac{a_{k+1}}{a_k}| \geq 1$ für alle $k \geq k_0$ gilt, dann ist $\sum^{\infty}_{k=1} a_k$ divergent
- Ist $\underset{k \rightarrow \infty}{lim} \sqrt[k]{|a_k|} = q < 1$, so ist $\sum^{\infty}_{k=1} a_k$ absolut konvergent
- Ist $\underset{k \rightarrow \infty}{lim} \sqrt[k]{|a_k|} = Q > 1$, so ist $\sum^{\infty}_{k=1} a_k$ divergent
- Existiert der Grenzwert $\underset{k \rightarrow \infty}{lim} |\frac{a_{k + 1}}{a_k}| = Q > 1$, so ist $\sum^{\infty}_{k=1} a_k$ divergent. Im Fall $q = Q = 1$ ist Konvergenz und Divergenz möglich.