---
tags: Uni RO
VL-Date: 17.05.23
---
# VHDL-Beschreibung von Zustandsautomaten
## D-Flip-Flop in [[VHDL]]
```VHDL
entity dff is
	port(d : in std_logic;
		q : out std_logic;
		Clk : in std_logic
	);
end entity dff

architecture rtl of dff is
begin
	process(clk)
begin
	if (clk’event and clk =1) then
		q <= d;
	end if;
end process;
end architecture rtl;
```
## Register bestehend aus D-Flip-Flops in VHDL
```VHDL
entity dff is
	port(d : in std_logic_vector(15 dowto 0);
		q : out std_logic_vector(15 dowto 0);
		Clk : in std_logic
		);
end entity dff

architecture rtl of dff is
begin
	process(clk)
	begin
		if (clk’event and clk =1) then
			q <= d;
		end if;
	end process;
end architecture rtl;
```

## Blockdiagramm repräsentiert die Struktur des VHDL-Codes

![[Blockdiagramm repräsentiert die Struktur des VHDLCodes.png|400]]

