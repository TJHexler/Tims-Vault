---
tags: Uni RO
VL-Date: 19.04.23
---
# Decoder mit Enable
## Ein 2:4 Decoder mit Enable
![[2zu4 Decoder mit Enable.png|400]]

### VHDL für einen 2:4 Decoder

```VHDL
-- 2-to-4-Line Decoder with Enable: Structural VHDL Description

library ieee, lcdf_vhdl;
use ieee.std_logic_1164.all, lcdf_vhdl.func_prims.all;
entity decoder_2_to_4_w_enable is
	port (EN, A0, A1: in std_logic);
end decoder_2_to_4_w_enable;
architecture dataflow_1 of decoder_2_to_4_w_enable is

signal A0_n, A1_n: std_logic;
begin
	A0_n <= not A0;
	A1_n <= A0_n and A1_n and EN;
	D1 <= A0 and A1_n and EN;
	D2 <= A0_n and A1 and EN;
	D3 <= A0 and A1 and EN;
end dataflow_1;
```

# Kombinatorische Schaltungen auf der Basis von Decodern
## Binärer Addierer
| X   | Y   | Z   | C   | S   |
| --- | --- | --- | --- | --- |
| 0   | 0   | 0   | 0   | 0   |
| 0   | 0   | 1   | 0   | 1   |
| 0   | 1   | 0   | 0   | 1   |
| 0   | 1   | 1   | 1   | 0   |
| 1   | 0   | 0   | 0   | 1   |
| 1   | 0   | 1   | 1   | 0   |
| 1   | 1   | 0   | 1   | 0   |
| 1   | 1   | 1   | 1   | 1    |
![[binaererAddiereraufBasisvonDecoder.png|300]]

## Prioritätscodierer
Priorotätscodierer ist eine kombinatorische Schaltung, die eine Prioritätsfunktion implementiert. Die Funktionalität des Prioritätscodierers ist folgendermaßen: Wenn zwei oder mehr Eingänge gleichzeitig den Wert 1 annehmen, das Eingangssignal mit der höchsten Priorität Vorrang hat.

| $D_3$ | $D_2$ | $D_1$ | $D_0$ | $A_1$ | $A_0$ | $V$ |
| ----- | ----- | ----- | ----- | ----- | ----- | --- |
| 0     | 0     | 0     | 0     | X     | X     | 0   |
| 0     | 0     | 0     | 1     | 0     | 0     | 1   |
| 0     | 0     | 1     | X     | 0     | 1     | 1   |
| 0     | 1     | X     | X     | 1     | 0     | 1   |
| 1     | X     | X     | X     | 1     | 1     | 1    |

## BCD zu Sieben-Segment Anzeige
![[BCD zu SiebenSegment Anzeige.png|200]]

### Implementierung mittels Logik-Gattern
$a = \overline{A}C+\overline{A}BD+\overline{B}\overline{C}\overline{D}+A\overline{B}\overline{C}$
$b = \overline{A}\overline{B}+\overline{A}\overline{C}\overline{D}+\overline{A}CD+A\overline{B}\overline{C}$
$c = \overline{A}B+\overline{A}D+\overline{B}\overline{C}\overline{D}+A\overline{B}\overline{C}$$
$d = \overline{A}C\overline{D}+\overline{A}\overline{B}C+\overline{B}\overline{C}\overline{D}+A\overline{B}\overline{C}+\overline{A}B\overline{C}D$
$e = \overline{A}C\overline{D}+\overline{B}\overline{C}\overline{D}$
$f = \overline{A}B\overline{C}+\overline{A}\overline{C}\overline{D}+\overline{A}B\overline{D}+A\overline{B}\overline{C}$
$g = \overline{A}C\overline{D}+\overline{A}\overline{B}C+A\overline{B}\overline{C}$
--> Eine Implementierung für jede boolesche Variable benötigt 27 AND-Gatter
--> Jedoch ist eine Mehrfachnutzung der Gatter möglich. Dadurch kann die Zahl der AND-Gatter auf 14 reduziert werden!