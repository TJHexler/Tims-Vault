---
tags: Uni RO
VL-Date: 03.05.23
---
# Ganze und Reelle Zahlen
Ganze Zahlen: Die Zahlenmenge ist unendlich aber diskret
- Es gibt keine Brüche
- Keine Zahlen zwischen aufeinanderfolgenden ganzen Zahlen:Integer
- Eine abzählbare endliche ) Anzahl an Zahlen zwischen zwei Zahlen

Reelle Zahlen : Die Zahlenmenge ist unendlich aber kontinuierlich
- Rationale Zahlen sind als Brüche darstellbar z.B ., 5/2 = 2.5
- Irrationale Zahlen sind nicht als Brüche darstellbar z.B ., Pi oder 2^0.5
- Es gibt eine unendliche Menge an Zahlen zwischen zwei reellen Zahlen

# IEEE 754 Floating Point Standart
- Exponent mit Bias: tatsächlicher Wertebereich (-127, 127) ändert sich in (0, 254):
	- __Exponent mit Bias__ beschreibt eine 8-Bit positive Binäre Ganzzahl (Integer)
	- Der tatsächliche Exponent wird durch die Subtraktion von $127_{10}$ oder $01111111_2$ ermittelt
- Das erste Bit des Mantisse entspricht immer dem Wert 1: $\pm 1.bbb...b*2^E$
- Die 1 vor dem Binärpunkt wird implizit vorausgesetzt
	- Die Mantisse ist ein 23-Bit-Bruch nach dem Binärpunkt
	- Der Wertebereich des Mantisse ist $[ 1,2)$

## Fließkommazahlen
- Format: $\pm 1.bbbbb_2 * 2^{eeee}$
- Wert: $(-1)^s*(1+F)*2^E$
Definitionen:
- S = Vorzeichen, 0 für positive, 1 für negative Zahlen
- F = Bruch
- M = Mantissenbitmuster wird interpretiert als pos. ganze Zahl mit p Bits.
- m = 1 + F = Mantisse (englisch auch als Significant bezeichnet).
- m = 1 + M/$2^p$
- B = Biaswert $B = 2^{r-1}-1$ bei Single Precision B = 127
- e = Exponent mit r Bits
- E = ist eine positive oder negative ganze Zahl
### Beispiel - IEEE 754

![[IEEE754Bsp.png|300]]

![[IEEE754Bsp2.png|300]]

#### Sonderfälle - IEEE 754


![[SonderfälleIEEE754.png|300]]

![[SonderfälleIEEE754.2.png|300]]

![[IEEE754DenormalisierteZahlen.png|300]]

## Fließkommazahlen Zusammenfassung

![[Fließkommazahlen.png|400]]

## Umwandlung Binär $\rightarrow$ Dezimal

![[UmwandlungBinärDezimalFliesskomma.png|400]]

### Beispiele

![[BeispielUmwandlungBinärDezimalFlieskommazahl.png|400]]

# Fließkomma Addition und Subtraktion
1. Nullprüfung - Wenn einer der Operanden den Wert 0 annimmt, bildet der jeweils andere Operand das Ergebnis
2. Bildung der Mantisse - Die Mantisse des kleineren Exponenten wird solange nach rechts geschoben bis beide Exponenten identisch sind
3. Addition - erfolgt durch die Addition der Mantissen. Erkennung eines Überlaufs
4. Normalisierung - Die Normalisierung erfolgt durch die Verschiebung der Bits der Mantisse Erkennung von Über- bzw. Unterlauf
5. Runden

#### Beispiel Subtraktion $0,5_{10} - 0,4375{10}$
1. zu addierende Zahlen sind ungleich null: $1,000_2 *2^{-1}$ und $-1,110_2 * 2^{-2}$
2. Mantisse des kleineren Exponenten wird nach rechts verschoben, bis sich beide Exponenten entsprechen $-1,110_2 * 2^{-2} \rightarrow -0,111_2 * 2^{-1}$
3. addiere Mantissen: $1,000_2 + (-0,111_2)$ Ergebnis: $0,001_2*2^{-1}$
4. Normalisieren von $1,000_2 *2^{-4}$ Es ist kein überlauf/Unterlauf zu erwarten, da gilt: $126 \geq exponent \geq - 126$
5. Das Runden der Werte bringt keine Änderung, da sie Summe in 4-Bits dargestellt werden kann $1,000_2 *2^{-4} = (1 + 0)/16 = 0,0625_{10}$ 

## IEEE 754 Guard- und Round-Bits
zwei zusätzliche Bits, die "Schutz-" bzw. "Rundungs-" Bit genannt werden (guard/round), werden für alle Zwischenadditionen verwendet.

Dies wird exemplarisch für die Addition von Fließkommazahlen im Dezimalsystem gezeigt. Mantisse mit drei Stellen:

![[IEEEGuardAndRoundBits.png|300]]

## IEEE 754 - Rundungsmodi

| Rundungsstrategie                                                                              | Beschreibung                                                                                                          |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Rundung in Richtung Null                                                                       | Die nächste repräsentierbare Zahl auf dem Zahlenstrahl von der erweiterten Zahl in Richtung zur Null wird verwendet.  |
| Rundung in Richtung $+\infty$                                                                  | Die nächste repräsentierbare Zahl auf dem Zahlenstrahlvon der erweiterten Zahl in Richtung +Unendlich wird verwendet. |
| Rundung in Richtung $-\infty$                                                                  | Die nächste repräsentierbare Zahl auf dem Zahlenstrahl von der erweiterten Zahl in Richtung Unendlich wird verwendet. |
| Rundung zur nächstgelegenen repräsentierbaren Zahl mit geringstem Abstand (Defaulteinstellung) | Die repräsentierbare Zahl, die den geringsten Abstand zur erweiterten Zahl hat, wird verwendet. Liegt die erweiterte Zahl genau in der Mitte zwischen zwei repräsentierbaren Zahlen, wird die Zahl genommen, deren niedrigste Ziffer gerade ist. |

# Multiplikation von Fließkomma-Zahlen
1. Separieren des Vorzeichen
2. Addition der Exponenten
3. Multiplikation der Mantissen
4. Normalisieren, Runden, Über/Unterlauf-Prüfung
5. Ersetzung des Vorzeichens
#### Beispiel $0.5_{10} * -0.4375_{10}$
entspricht binär: $1.000_2*2^{-1} * -1.110_2*2^{-2}$
1. Addition der Exponenten: $-1 + (-2) = -3$
2. Multiplikation der Mantissen: $1.000 * 1.110 = 1.110000$
3. Normalisieren: Wenn nötig, wird die Mantisse nach rechts verschoben und der Exponent erhöht. Das normalisierte Produkt lautet $1.110000*2^{-3}$ (Dezimahlzahl = $-(1+0.5+0.25)/8 = -0.21875_{10}$)

## Division von Fließkommazahlen
- Separieren des Vorzeichens
- Überprüfen der Sonderfälle: Null oder Unendlich
- Subtraktion der Exponenten
- Division der Mantissen
- Normalisieren und Detektion eines Über-/Unterlaufs
- Runden
- Ersetzen des Vorzeichens
