---
tags: Uni RO
VL-Date: 19.04.23
---
# CMOS-Logik
## Realisierung mittels Transistoren
Complementary Metal-Oxide-Semiconductor, CMOS, ist eine Bezeichnung für Halbleiterbauelemente, bei denen sowohl p-Kanal- als auch n-Kanal-Transistor auf einem gemeinsamen Substrat (Chip) verwendet werden.
Unter CMOS-Technologie werden zwei Dinge verstanden:
- Verwendeter Halbleiterprozess zur Realisierung von integrierten digitalen Schaltungen.
- Logikfamilie, die CMOS-Logik stellt heutzutage die meistgenutzte Logikfamilie
Die CMOS-Logik besteht aus zwei Arten von Transistoren, die wir als Schalter betrachten:
- N-Kanal-Transistor
- P-Kanal-Transistor

## CMOS Gatter
![[CMOSGatter.png]]
- "Vdd" ist die positive Versorgungsspannung (Pluspol der Batterie)
- GND Ground Erdung


Das Pull-Up/Down-Netzwerk ist die Realisierung der Booleschen Funktion $f_N = f_N (x_1,x_2,...,x_{n-1}), f_P = f_P(x_1^{`},...,x_{n-1}^{`})$ unter der Verwendung von Schaltern

![[CMOSGatterFunktionen.png|400]]
### Bestimmung der Funktionen: $f_N, f_P$

![[CMOSGatterBestimmungderFunktionen.png|400]]

### Beispiel NAND-Gatter
![[CMOS NAND Gatter.png|400]]

## Halbaddierer und Volladdierer mit CMOS
![[Halbaddierer und Volladdierer mit CMOS.png|400]]

### Volladdierer
s <= a xor b xor d; c <= (a and b) or (a and d) or (b and d);
![[Volladdierer mit CMOS.png|400]]

