---
tags: Uni RO
VL-Date: 03.05.23
---
# Volladdierer
Funktioniert wie ein [[Halbaddierer]], mit drei Eingängen: $a,b, d$.
$d$ wird oft auch $c_{i-1}$ genannt (Carry vom vorherigem Volladdierer).
## Halbaddierer - Volladdierer
![[HalbaddiererUndVolladdierer.png|200

## Volladdierer auf Gatterebene
$S = a \oplus b \oplus d$
$C = (ab) + (ad) + (bd)$

![[Volladdiererschaltung.png|250]]

$\overline{c_i} = \overline{a_i*b_i + a_i * c_{i-1} + b_i * c_{i-1}}$ 
Die Summe $S_i$ und das invertierte Carry $\overline{C_i}$ sind identisch mit der Ausnahme von zwei Fällen ($a_i, b_i, c_{i-1} = 0/1$).
Somit kann man $S_i$ auch anders darstellen:
$S_i = (a_i + b_i + c_{i-1})*\overline{c_i} + a_i * b_i * c_{i-1}$  

Damit ergibt sich folgendes effizientes CMOS-Gatter:
![[Volladdierer CMOSGatter effizient.png|300]]

Für Carry und Summe des Volladdierers:
$f(\overline{a_i}, \overline{b_i}, \overline{i_{i-1}}) = \overline{f} (a_i, b_i, c_{i-1}) \Rightarrow f_N = f_P$
__Identisches Pull-Up und Pull-Down Netzwerk!__

![[VolladdiererInCMOS.png|300]]

Transistorzahlen: 24 Transistoren + 4 Transistoren für Inverter = __28 Transistoren__

## [[VHDL]] Full Adder

```VHDL
library ieee;
use ieee.std_logic_1164.all;

entity full_adder is
port(
	A : in std_logic
	B : in std_logic
	C0 : in std_logic
	C1 : out std_logic
	S : out std_logic)
end entity full_adder;

architecture logic arch of full_adder is
begin
	S <= A xor B xor C_in;
	C1 <= (A and B) or (A and C0) or (B and C0);
end architecture logic arch;
```