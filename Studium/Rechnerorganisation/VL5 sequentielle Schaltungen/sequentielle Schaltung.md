---
tags: RO Uni
VL-Date: 10.05.23
---
# sequentielle Schaltungen
- Sequentielle Schaltungen beinhalten Speicher und besitzen einen sogenannten internen Zustand
- Kombinatorische Logik oder Schaltungen besitzen keinen Speicher, die Ausgangswerte kombinatorischer Schaltungen sind lediglich von den Eingangswerten abhängig
- Die Ausgangswerte einer sequentiellen Schaltung hängt von den aktuellen Eingangswerten sowie den internen Zuständen der sequentiellen Schaltung ab.
- Die Zustände sequentieller Logik hängt von vergangenen Eingangswerten bzw. der Sequenz der Eingangswerte ab.
## Timing Analyse
Gatterverzögerung: Maximale Verzögerung $d$ von allen Eingängen zu allen Ausgängen (Und-Gatter: 0,5ns und Inverter: 0,3ns)
### Timing-Modell eines Flip-Flops
![[Timing-Modell eines Flip-Flops.png|300]]
### statische Timing Analyse
Erzeugung eines Timing-Graphen durch das Entfernen aller Flip-Flops und Ergänzung der Knoten mit Setup-Time und CK-Q-Time
Kritischer Pfad: maximale Laufzeit

### Timing-Optimierung sequentieller Schaltungen
sind Schaltungen sequentiell nacheinander geschaltet, kann die Taktrate erhöht werden, in dem man zwischen jede Pipeline-Ebene ein [[Flip-Flop]] einfügt. (Latenz steigt dafür)

### Schieberegister in VHDL
```VHDL
library ieee;
use ieee.std_logic_1164. all;
entity shift_right_register is
	port
		clk, reset : in std_logic;
		d: in std_logic
		q: out std_logic
	);
end shift_right_register;

architecture two_seg_arch of shift_right_register is
signal r_reg : std_logic_vector (3 downto 0);
signal r_next : std_logic_vector (3 downto 0);
	-- register
begin
	process(clk,resetI)
	begin
		if(reset =‘1‘) then
			r_reg <= ( others => 0)‚
		elsif (clk‘event and clk =‘1‘) then
			r_reg <= r_next
end process;
--next-stable logic (shift right 1 bit)
r_next-state logic (shift right 1 bit)
r_next <= d & r_reg (3 downto 1);
--output
q <=r_reg(0);
end two_seg_arch;
```

### Beispiele sequentieller Schaltungen
#### universelles Schieberegister
- Operationen: Laden, Verschiebung nach recht (right shift)
- Verschiebung nach links (left shift)
- Pause

##### universelles Schieberegister in VHDL
  ```VHDL
  library ieee;
use ieee.std_logic_1164. all
entity shift_register is
port ()
	clk, reset : in std_logic;
	ctrl: in std_logic_vector (1 downto 0);
	d: in std_logic_vector 3 downto 0
	q: out std_logic_vector (3 downto 0)
	);
end shift_register

architecture two_seg_arch of shift_register is
	signal r_reg : std_logic_vector (3 downto 0);
	signal r_next : std_logic_vector (3 downto 0);
begin
--register
process(clk,reset)
	begin
		if (reset =‘1‘) then
			r_reg <= ( others => 0)
		elsif (clk‘event and clk =‘1‘) then
			r_reg <= r_next
end if
end process
--
next state logic
with
ctrl select
r_next
r_reg when "00". -pause
when ctrl select
	r_req(2 downto 0) & d(0) when "01": -shiftl
	d(3)&r_req(3 downto 1) when "10". shift r
	d when others -load
-output logic
q <= r_req;
end two_seg_arch
```

### freilaufender Zähler
VHDL Code siehe Folien Kapitel 5 Teil 3 Folie 16
### Binärzähler
VHDL Code siehe Folien Kapitel 5 Teil 3 Folie 18
