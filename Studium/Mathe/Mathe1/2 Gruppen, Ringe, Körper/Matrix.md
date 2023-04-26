---
tags: Uni Mathe
---
# 2.3 Matrizen

Eine $n \times m$ Matrix mit Einträgen in einem Ring $R$ ist ein rechteckiges Schema
$$\begin{pmatrix}a_{11} & \cdots & a_{1m}\\\vdots & \ddots & \vdots\\a_{n1} & \cdots & a_{nm}\end{pmatrix}$$
von Elementen$a_{i, j} \in R$ die in einer Tabelle mit $n$ Zeilen und $m$ Spalten angeordnet sind. Man sagt, $i$ ist der Zeilenindex und $j$ der Spaltenindex des Eintrags $a_{ij}$ . Die Menge der $n×m$-Matrizen mit Einträgen in $\mathbb{R}$ wird mit $M_{n,m}(R)$ bezeichnet. Die obige Matrix wird auch mit $(a_{ij} )$ bezeichnet.

## Matrixmultiplikation
Sind $A$ und $B$ zwei Matrizen mit Einträgen aus dem selben Ring $\mathbb{R}$ und stimmt die Spaltenanzahl $n$ von $A$ mit der Zeilenanzahl von $B$ überein, so kann man das Matrizenprodukt $AB$ als die Matrix definieren, deren Eintrag in der i-ten Zeile und j-ten Spalte durch $\sum_{k=1}^{n} a_{ik}b_{kj}$ gegeben ist.

Wie man leicht nachprüft, gilt hier $AB \neq BA$, die Matrixmultiplikation ist also __nicht kommutativ__. 

## Addition
Die Summe $A + B$ wird durch die komponentenweise Addition definiert, d.h. der Eintrag in der i-ten Zeile und j-ten Spalte von $A + B$ ist $a_{ij} + b_{ij}$

Die Menge $M_{n, m}$ der $n \times m$ Matrizen mit Einträgen in $R$ wird mit dieser Addition zu einer abelschen Gruppe mit der __Nullmatrix__ (alle Einträge sind Null).

## Die Einheitsmatrix
Das Einselement des Ring mit Eins der quadratischen Matrizen ist gegeben durch:
$$E := E_n \begin{pmatrix}a_{11} & \cdots & a_{1m}\\\vdots & \ddots & \vdots\\a_{n1} & \cdots & a_{nm}\end{pmatrix}$$
Die Einträge der Einheitsmatrix kann man auch durch das sogenannte __Kronecker-Symbol__ beschreiben: $E_n=\left(\delta_{ij}\begin{cases}1, & \text{falls }i=j\\0, & \text{falls }i\neq j\end{cases}~\right)$

## Hilfssatz 2.3.2 
Mati