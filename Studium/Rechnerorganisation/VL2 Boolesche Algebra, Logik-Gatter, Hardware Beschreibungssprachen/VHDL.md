---
tags: Uni RO
VL-Date: 19.04.23
---
# VHDL
## VHDL-Logikoperationen

Die Hardware-Beschreibungssprache VHDL (HDL = Hardware Description Language)
| Logischer Operator | (VDHL) Beispiel |
| ------------------ | --------------- |
| not                | F <= not X;     |
| and                | F <= X and Y;   |
| or                 | F <= X or Y;    |
| nand               | F <= X nand Y;  |
| nor                | F <= X nor Y;   |
| xor                | F <= X xor Y;   |
| xnor               | F <= X xnor Y;  |

# Hardware-Beschreibungssprache VHDL

VHDL = VHSIC Hardware Description Language
VHSIC = Very High Speed Integrated Circuit
In the VHSIC-Program in 1981 IBM, TI and others developed chips for the US Department of Defense (1983 first VHDL version)

## Ein erstes Beispiel in VHDL

```VHDL
entity compare is
	port (a_i, b_i : in std_ulogic_vector (7 downto 0);
		eq_o : out std_ulogic );
end compare;

architecture rtl of compare is
begin
	eq_0 <= '1' when ( a_i = b_i ) else '0';
end rtl;
```

Was in der Architektur steht ist die Funktion
Beispiel wird realisiert durch 8 XNOR Gatter für jeweils $a_i, b_i$ die anschließend alle UND-verknüpft werden.

## Unterschied VHDL zu Programmiersprache wie C, C++

- VHDL modelliert Hardware-Architekturen auf Taktzyklenebene (Modell der Zeit)
- sequentielle Programmierung C, C++ kennt nur Datenabhängigkeiten (keine Modellierung der Zeit)
- VHDL: alle Anweisungen werden parallel ausgeführt (außerhalb von Prozessen)
- Compiler für zwei Dinge: Simulation und Synthese
- man interessiert sich für das Ergebnis der Synthese (Taktrate, Anzahl der verwendeten Ressourcen wie Gatter)
- Erzeugung einer Schaltung mit einem Hardware-Baustein (Field Programmable Gate Array)

## Themen in RO1
- VHDL: nur Logikschaltungen keine sequentielle Schaltungen
- nur lesen (und ergänzen) von vorhandenem VHDL-Code
- Verwenden von Schaltungen auf dem FPGA-Board auf Basis eines VHDL-Codes (Hardware-Taschenrechner)
- Erlernen eines Instruction-Sets eines FPGA-Mikrocontrollers

## Zahlensysteme
- Integer und Float
- Überlauf
- Konvertierung
- Besonderheiten von Typen Integer: (Zahl in Zweierkomplementdarstellung) und Float

