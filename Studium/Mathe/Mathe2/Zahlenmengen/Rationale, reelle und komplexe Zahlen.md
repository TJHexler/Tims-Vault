---
tags: Uni Mathe
VL-Date: 14.04.23
---
# Rationale, reelle und komplexe Zahlen

Definition
Wir definieren die rationalen Zahlen als die Menge der endlichen d...Dezimalbrüche

## Einige wichtige Eigenschaften der rationalen Zahlen

1. Die Menge ist total geordnet, d.h. für je zwei verschiedene rationale Zahlen lässt sich angeben, welche die kleinere ist.
2. Die Menge Q ist überall in sich "dicht", d.h. ... zwei verschieden rationalen Zahlen liegt mindestens eine weitere. Daher liegen zwischen zwei rationalen Zahlen unendlich viele weitere ... Zahlen.
3. Q ist ein [[Körper]], d.h. die Operationen Addition, Subtraktion Multiplikation und Division, außer durch 0, sind in Q enthalten
## wie viele rationale Zahlen gibt es?

Man nennt eine unendliche Menge M abzählbar, wenn es eine bijektive [[Abbildung]] N -> M gibt.
### Bemerkung
Q ist abzählbar.
### Beweisskizze:
...
Während man m uneingeschränkt Potenzieren q -> $q^n$, nicht in Q kann ist ... , also Wurzelziehen nicht ... möglich, denn z.B.
#### Beispiel
$root{2}$ ist irrational
#### Beweis
Angenommen, es gäbe ein $q element Q$ mit $q^2 = 2$, sei $q = a/b$ mit $a, b$ teilerfremd. Angenommen, $2=q^2=a^2/b^2$, dann folgt $2b^2=a^2$, also muss $a$ gerade Zahl sein, wir setzen $a= 2k$ und erhalten $2b^2=4k^2$ und somit $b^2=2k^2$, also auch b gerade, Widerspruch zu teilerfremdheit von $a$ und $b$.
Um dies zu beheben, nehmen wir die __irrationalen Zahlen__, gegeben als nicht -periodische Dezimalbrüche zu Q dazu und erhalten die Menge der reellen Zahlen R.
# Reelle Zahlen
## Satz 2.1
R ist __überabzählbar__, d.h. nicht abzählbar unendlich.
### Beweisskizze: 
Angenommen, es gäbe eine abzählbare "Liste" der reellen Zahlen im Intervall $[0,1]$ 
1. 0,1544264...
2. 0,4548943...
3. 0,5498432...
- ...
Wir zeigen: Es gibtr eine weitere Zahl, in $[0,1]$, die nicht auf der Liste ist. Nämlich die Zahl, die wir erhalten, wenn wir die "__Diagonale__" betrachten und die Ziffern dort abändern, z.B.: steht dort eine Ziffer, die von Null verschieden ist, nehmen wir Null, sonst 1.
Im Beispiel: 0,000000...
Widerspruch, also ist R nicht abzählbar.
## Mächtigkeiten
$|N|=|Q|<|R|=|Pot(N)|
## Einige Haupteigenschaften der reellen Zahlen
1. R ist total geordnet.
2. Q liegt dicht in R, beliebig nahe an ... reellen Zahl liegt eien rationale Zahl. Sei $xelementR$, dann gilt: $FürAlleEpsilon>0ExistiertqelementQ: |x-q|<epsilon$ 
3. Die reellen Zahlen sind ein __Kontinuum__, d.h. sie füllen die Zahlengerade lückenlos aus. Vollständigkeit, jede Intervallschachtelung $[a,b] )_ [a_2, b_2] )_ [a_3, b_3]$ hat nicht leeren Durchschnitt ...
4. R ist ein [[Körper]], Potenzieren $x->x^n$ und ... $x-->nteroot{x}$ ist für $x>=0$ und ... uneingeschränkt möglich
Was es nicht in R gibt, sind z.B. Quadratwurzeln negativer Zahlen.
# Die komplexen Zahlen C
Um Nullstellen von Polynomen bestimmen zu können und ein Wurzeln aus negativen Zahlen ziehen zu können, ... die komplexen Zahlen.
## Def. 2.2
Die Menge der komplexen Zahlen wird definiert als C = R x R, als Menge von Paaren (a,b) von reellen Zahlen, auf den folgende Verknüpfungen eingeführt sind:
Addition...
Multiplikation...
R ist eine echte Teilmenge von C, ...
Wir führen die imaginäre Einheit $i$ ein, als $i=(0,1)$, damit gilt $i^2=(-1,0)$
Manchmal ... man auch $i=...$
## Satz 2.3
Für jede komlexe Zahl z element C gilt $z = (a,b) = a + ib$, mit a, b element R und diese Darstellung ist eindeutig.
### Beweis
$(a,0)+(0,1)(b,0)=(a,0)+(0,b)=(a,b)$
Die komplexen Zahlen bilden einen [[Körper]].
## Definition 2.4
Sind $a,b \in R, z = a+ib element C$, dann nennt man a den __Realteil__ und b den __Imaginärteil__ von z.
Die komplexen Zahlen $C=R^2$ können als Zahlenebene aufgefasst werden, dann ist die Addition die Vektoraddition.
Bild
Multiplikation mit i bedeutet 90° Drehung im Koordinatensystem.
Die Spiegelung an der x-Achse = reellen Achse wird komplexe __Konjugation__ genannt, ist $z=a+ib$, dann definiert man:
$strichüberi = a-ib$ 
## Satz 2.5
Für $z,w \in C$ gilt:
1. $strichüberz+w = strichüberz + strichüberw$
2. $strichüberzw = strichüberz * strichüberw$ 
3. $z + strichüberz = 2Re(z)$ und $z - strichüberz = 2Im(z)$
4. $zstrichüberz$ ist eine nicht negative reelle Zahl
### Beweis...
Die zahl $|z| = root(z*strichüberz) = root(a^2+ b^2)$ mit $r=|z|$ und sei phi der Winkel... von z zur x-Achse, dann ... immer:
$z = r(cos(phi) + i sin(phi))$, __Polardarstellung__
Insbesondere gilt:
$r(cos(phi)+ i sin(phi)) * s(cos(ro) + i sin(ro)) =$
$rs(cos(phi)cos(ro) - sin(phi)sin(ro) + i (cos(phi)sin(ro)+sin(phi)cos(ro))$ 
