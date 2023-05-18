---
tags: RO Uni
VL-Date: 10.05.23
---
# Einführung - Schaltungsprinzipien für Informationsspeicherung
## Bistabile Kippstufe - RS-Flip-Flop
### Wie werden Informationen gespeichert
#### Dynamischer Speicher
Informationsspeicherung durch Ladungsspeicherung auf Kapazität
Entladungen durch nicht perfekte Isolierung: Auffrischen der Ladungen
#### Statischer Speicher
Informationsspeicherung mittels rückgekoppelten Inverterpaar
Bei zwei stabilen Zuständen spricht man von einer bistabilen Kippstufe (Flip-Flop)

#### Flip-Flop-Historie
William Henry Eccles (1875 1966) Physiker war ein Pionier auf dem Gebiet
der Funkübertragungstechnik am City and Guilds Technical College in London
Eccles Jordan circuit Erfindung sowie Implementierung erfolgten im Jahre 1919 Anwendung : Realisierung einer Schaltung für atmosphärische Turbulenzen ausgelöste Störungen des Radios

### Flip-Flop mit Setzeingang
Das Flip-Flop wird mit "0" am Eingang $\overline{S}$ gesetzt, d.h. $Q=1$.
Das Flip-Flop wird mit "1" am Eingang $overline{S}$ nicht beeinflusst, da dann $X*\overline{S} = X$.
![[Flip-Flop mit Setzeingang.png|200]]
### Flip-Flop mit Rücksetzeingang
Das Flip-Flop wird mit "0" am Eingang $\overline{R}$ zurückgesetzt: $Q=0$.
Das Flip-Flop wird mit "1" am Eingang $\overline{R}$ nicht beeinflusst, da dann $X*\overline{R}=X$.
![[Flip-Flop mit Rücksetzeingang.png|200]]
### RS-Flip-Flop
![[RS-FlipFlop.png|200]]
| Eingang   | $\overline{S}$ | $\overline{R}$ | Q   | $\overline{Q}$ |
| --------- | -------------- | -------------- | --- | -------------- |
| Reset     | 1              | 0              | 0   | 1              |
| Set       | 0              | 1              | 1   | 0              |
| Speichern | 1              | 1              | Q   | $\overline{Q}$ |
| Vermeiden | 0              | 0              | kA  | kA               |

### Getaktetes RS-Flip-Flop
![[getaktetes RS-FlipFlop.png|100]]
Speichern bei $C=0$, transparent bei $C=1$.

### D-Latch
Datenspeicherung mit $D=S=1/0$ und $\overline{D}=R=0/1$
![[D-Latch.png|200]]
![[D-Latch Diagramm.png|200]]
- level-sensitiv (die Operation hängt vom Pegel des Clk-Signals ab)
- nicht geeignet für den üblichen sequentiellen Schaltungsentwurf

#### Multiplexer als D-Latch
![[Multiplexer D-Latch.png|200]]
#### Vergleich D-Latch Realisierungen
![[D-Latch Realisierungen Vergleich.png|200]]

#### Datenspeicherung für eine Taktperiode
![[Datenspeicherung für eine Taktperiode.png|350]]
Speicherung für eine Taktperiode durch Serienschaltung von L1 und L2.

## D-Flip-Flop
![[D-Flip-Flop.png|300]]
- wird aktiviert wenn das Taktsignal sich von 0 auf 1 ändert, d.h. bei der steigenden Taktflanke (sonst Wert unverändert)
### Realisierung mit Multiplexern
![[D-Flip-Flop Multiplexer.png|200]]
### Setup- and Hold-Time eines D-Flip-Flop
![[Setup- Hold-Time D-Flip-Flop.png|300]]
### D-Flip-Flop in VHDL
```VHDL
entity dff is
	port (d : in std_logic;
		q : out std_logic;
		Clk: in std_logic
		);
end entity dff;

architecture rtl of dff is 
	begin
		process(clk)
		begin
			if (clk`event and clk = 1) then
			q <= d;
		end if;
	end process;
end architecture logic-arch
```

## Flip-Flop Typen
![[Flip-Flop-Typen.png|300]]
