---
tags: Uni RO
VL-Date: 19.04.23
---
# Multiplexer
Ein Multiplexer ist eine kombinatorische Schaltung, die binäre Information aus mehreren Eingängen (I0,I1) auswählt und die Information an eine einzige Ausgangsleitung Y übergibt. Die Auswahl wird von einer bestimmten Eingangsleitung wird von Eingangsvariablen (S) gesteuert.
![[Multiplexer2zu1.png|100]]
## 2:1 Multiplexer
| S   | $I_0$ | $I_1$ | Y   |
| --- | ----- | ----- | --- |
| 0   | 0     | 0     | 0   |
| 0   | 0     | 1     | 0   |
| 0   | 1     | 0     | 1   |
| 0   | 1     | 1     | 1   |
| 1   | 0     | 0     | 0   |
| 1   | 0     | 1     | 1   |
| 1   | 1     | 0     | 0   |
| 1   | 1     | 1     | 1   |

![[Multiplexer Schaltungsplan.png|300]]

## 4:1 Multiplexer
| $S_1$ | $S_0$ | Y     |
| ----- | ----- | ----- |
| 0     | 0     | $I_0$ |
| 0     | 1     | $I_1$ |
| 1     | 0     | $I_2$ |
| 1     | 1     | $I_3$      |

![[Multiplexer4zu1Schaltungsplan.png|300]]

--> Entwurf auf Gatter Ebene ist zeitaufwändig --> Hardware-Modellierungssprache --> ähnlich zu Programmierung Software --> Compiler: Gatter-Netzliste

## VHDL-Beschreibung: 4-to-1 Multiplexer
```VHDL
library ieee;
use ieee.std_logic_1164.all;
entity multiplexer_4_to_1_we is
	port (S : in std_logic_vector(1 downto 0);
		I : in std_logic_vector(3 downto 0);
		Y : out std_logic);
end multiplexer_4_to_1_we;

architecture dataflow_1 of decoder_2_to_4_w_enable is
begin
	Y <= I(0) when S = "00" else
		I(1) when S = "01" else
		I(2) when S = "10" else
		I(3) when S = "11" else
		'X';
end function_table;
```
