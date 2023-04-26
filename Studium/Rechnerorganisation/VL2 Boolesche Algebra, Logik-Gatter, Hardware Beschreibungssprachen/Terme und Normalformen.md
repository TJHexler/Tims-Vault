---
tags: Uni RO
VL-Date: 19.04.23
---
# Terme
## Definitionen
- **Produktterm**: einfache Variablen oder Konjunktion mehrerer ggf. negierter Variablen
- **Summenterm**: einfache Variablen oder Disjunktion mehrerer ggf. negierter Variablen
- **Minterm**: Produktterm, in dem jede Variable einer booleschen Funktion genau einmal vorkommt
- **Maxterm**: Summenterm, in der jede Variable einer booleschen Funktion genau einmal vorkommt
- **Summe von Produkten**: einzelner Produktterm oder Disjunktion mehrerer Produktterme
- **Produkt von Summen**: einzelner Summenterm oder Konjunktion mehrerer Summenterme
- **Disjunktive Normalform (DNF)**: eindeutige Darstellung einer booleschen Funktion f als Disjunktion aller Minterme m mit f(m)=1.
- **Konjunktive Normalform (KNF)**: eindeutige Darstellung einer booleschen Funktion f als Disjunktion aller Maxterme m mit f(m)=1.
- Aus einer DNF (KNF) kann eine möglichst einfache, d.h. minimale Summe von Produkten generiert werden:
	- Wiederholte Anwendung von Axiomen u. Theoremen der Booleschen Algebra
	- Verwendung von Karnaugh-Diagrammen
	- Algorithmische Minimierung auf dem Rechner

## Summe der Minterme
| X   | Y   | Z   | Symbol |
| --- | --- | --- | ------ |
| 0   | 0   | 0   | $m_0$  |
| 0   | 0   | 1   | $m_1$  |
| 0   | 1   | 0   | $m_2$  |
| ... | ... | ... | ...       |
$F = \overline{X}\overline{Y}\overline{Z}+\overline{X}Y\overline{Z}+X\overline{Y}Z+XYZ=m_0+m_2+m_5+m_7=\sum{m(0, 2, 5, 7)}$

## Produkt der Maxterme

| X   | Y   | Z   | Symbol |
| --- | --- | --- | ------ |
| 0   | 0   | 0   | $M$    |
| 0   | 0   | 1   | $M_1$  |
| 0   | 1   | 0   | $M_2$  |
| ... | ... | ... | ...    |
$M_0$ bedeuted: X oder Y oder Z

## Summe von Produkttermen
Die Umwandlung in eine Produktsumme erfolgt durch das Anwenden des Distributivgesetzes $F = AB + C(D + E) = AB + CD + CE$
#### Dreistufige und zweistufige Iimplementierung
![[2und3stufigeImplementierungderselbenFunktion.png|300]]

