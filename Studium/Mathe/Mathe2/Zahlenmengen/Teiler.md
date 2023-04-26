---
tags: Uni Mathe
VL-Date: 12.04.23
---
# Teilbarkeit
Der Begriff Teiler einer ganzen Zahl ist aus der Schule bekannt.
## Definition 1.33
Sei $n \in \mathbb{Z} , m \in \mathbb{N}$. Die Zahl $m$ heißt __Teiler__ von $n$, in Zeichen $m | n$, wenn 
$\exists k  \in \mathbb{Z} : km = n$

In diesem Fall heißt $n$ teilbar durch $m$
Es gilt:
- Die Zahl $0$ ist durch alle $m$ teilbar.
- Ist $m|n_1, m|n_2$ dann folgt $m|(n_1 + n_2)$

## Definition 1.34
Sei $a \in \mathbb{Z}$. Die Menge aller Teiler ist $D(a) = \{ d \in \mathbb{N} : d|a \}$
Seien $a, b \in \mathbb{Z}$. Die Menge aller gemeinsamen Teiler von $a$ und $b$ ist $D(a, b) = D(a) \cap D(b)$.

Die Zahl $ggt(a, b) := max\{ d  \in D(a) \cap D(b) \}$ heißt __größter gemeinsamer Teiler__ von a und b.

# Berechnung des größten gemeinsamen Teilers
Sind $a$ und $b \in \mathbb{N} , a < b$, dann gibt es natürliche Zahlen $q, r$ mit $0 <= r<b$ und $a = qb + r$
## Hilfssatz
Seien $a, b \in \mathbb{N}, a = qb + r$. Dann ist 
- $D(a, b) = D(b, r)$
- $ggT(a, b) = ggT(b, r)$
### Beweis
Ist $d \in D(a,b)$, d.h. $d|a \wedge d|b$,dann gilt $d|r$ mit $r = a - qb$. Damit ist $d \in D(b,r)$.
Umgekehrt, sei $d \in D(b, r)$ d.h. $d|b \wedge d|r$. Dann ist $d|a \wedge d  \in D(a,b)$.

## Euklidischer Algorithmus zur Berechnung von ggT(a, b)
Starte mit (a, b)
1. Teste, ob $b|a$
2. Wenn ja: $D(a, b) = D(b)$ und $ggT(a, b) = b$; Stopp.
3. Wenn nein: Teile mit Rest $a = qb + r, 0 < r < b$. Zurück zum Anfang mit dem Paar (b, r).