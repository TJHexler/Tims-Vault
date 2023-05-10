---
tags: Uni RO
VL-Date: 03.05.23
---
# Carry-Ripple-Addierer

![[CarryRippleAddierer.png|400]]

## [[VHDL]] Carry-Ripple

```VHDL
entity ripple_carry_adder is
port(
	A :in std_logic_vector (3 downto 0);
	B :in std_logic_vector (3 downto 0);
	C0:in std_logic;
	S : out std_logic_vector (3 downto 0);
	C4: out std_logic);
end entity ripple_carry_adder;

architecture structure of ripple_carry_adder is
	signal C : std_logic_vector(4 downto 0);
begin -- architecture structural
	C(0) <= C0;
	ripple_adder_generation : for i in 0 to 3 generate
		full_adder_I : entity work.full_adder
		port map (
		A => A(i),
		B => B(i),
		Cin => C(i),
		Cout => C(i+1),
		S => S(i));
	end generate ripple_adder_generation;
	C4 <= C(4);
end architecture structure;
```
generate instanziiert die angegebene Zahl von Volladdieren.

Man kann auch den Carry-Ripple-Addierer in VHDL mittels logischer Ausdrücke für jeden einzelnen Ausgang benutzen, das ist dann zwar sehr unübersichtlich, aber möglicherweise schneller.

### VHDL-Behavioral Style Carry-Ripple
```VHDL
library ieee;
use ieee.std_logic_1164.all;
use ieee.std_logic_unsigned.all;
-- provides unsigned numerical computation on type std_logic_vector

entity ripple_carry_adder is
port (
	A : in std_logic_vector (3 downto 0);
	B : in std_logic_vector (3 downto 0);
	C0 : in std_logic
	S : out std_logic_vector (3 downto 0);
	C4 : out std_logic
end entity ripple_carry_adder;

architecture beh of ripple_carry_adder is
signal sum : std_logic_vector (4 downto 0);
begin
	sum <= ('0' & A) + ('0' & B) + C0;
	C4 <= sum(4);
	S <= sum(3 downto 0);
end architecture beh;
```
