---
tags: Uni RO
VL-Date: 17.05.23
---
# Zustandsautomaten
- engl. "Finite State Machines" (__FSM__)
- zur Steuerung von Abläufen z.B. in digitalen Schaltungen, in Mikroprozessoren oder Mikrocontrollern verwendet
- werden im folgenden als sequentielle Schaltung realisiert
- 5 Komponenten:
  1. Zustandsspeicher
  2. Eingangssignale
  3. Ausgangssignale
  4. Übergangsfunktion der Zustände (Übergang in den nächsten Zustand) (abhängig von aktuellem Zustand und den Eingangssignalen)
  5. Ausgabefunktionen
- klassisches Bsp.: Ampel

## Blockdiagramm sequentieller Schaltungen von FSMs
![[Blockdiagramm sequentieller Schaltungen von FSMs.png|300]]

## Zustandsdiagramme und Entwurf von FSMs
### Entwurf
1. Festlegung der Zustände, Ein- und Ausgänge
2. Festlegung des Zustandsdiagramms
3. Festlegung der Zustandscodierung
4. Bestimmung der Übergangslogik zwischen dem aktuellem und dem nächstem Zustand
5. Bestimmung der Mealy- und Moore-Ausgabe-Logik

### Beispiel Ampel
![[AmpelZustandscodierung.png|300]]

## D-Flip-Flops zum Speichern der Zustände
Verzögerung um eine Taktperiode
Zustandswechsel mit der steigenden Taktflanke
![[DFlipFlopVerzögerungTaktperiode.png|300]]

### Zustandsübergänge
![[ZustandsübergängeRO.png|300]]
Vereinfachung der Booleschen Ausdrücke möglich

## Zustandsübergangslogik
![[ZustandsübergangslogikRO.png|300]]

![[ZustandsübergangslogikRO2.png|150]]
beim vollständigen Zustandsdiagramm fällt auf: Die unerwünschten Zustände werden nie verlassen!
$\rightarrow$ Angabe vollständiger Zustandsdiagramme bei dem Entwurf des Zustandsautomaten vermeidet unerwünschtes Verhalten.
![[ZustandsübergangsdiagrammRO.png|300]]

Auswahl einer anderen Zustandscodierung:
![[ZustandscodierungAmpelBesser.png|300]]

## Zustandsübergangslogik
$A = \overline{a} * b + a * \overline{b}$
$B = \overline{b}$
![[ZustandsuebergangslogikAmpelBesser.png]]

## Zustandscodierung
![[ZustandscodierungAmpelBesserAusgänge.png|300]]
![[GatterschaltungAmpelBesser.png]]


# Zustandsübergang mit Gatterverzögerung
Annahme zur Vereinfachung: Einheitsverzögerung $\Delta$ der Gatter
![[Zustandsübergang mit Gatterverzögerung.png|300]]

So würde für $\Delta < t < 2 \Delta$ Also zwischen Rot und Gelb Rot kurzzeitig Grün angezeigt werden!
Abhilfe: __Flipflops__ (FF) an den Ausgängen $\rightarrow$ keine Zwischenzustände am FF-Ausgang.

![[BlockdiagrammSequentiellerSchaltungenVonFSMs.png|400]]

# Formale Definition von Zustandsautomaten
- endliche Menge A von Eingabesymbolen $a_i \in A$(Alphabet)
- endliche Menge S von Zuständen $s_i \in S$
- Anfangszustand $s_0 \in S$
- Zustandsübergangsfunktion $\delta : S \times A \rightarrow S$
weiterhin kann er umfassen
- endliche Menge B von Ausgabesymbolen $b_i \in B$
- Ausgabefunktion $\lambda : S \times A \rightarrow B$ (Mealy Variante)
- Ausgabefunktion $\lambda : S \rightarrow B$ (Moore Variante)

- jeder Zustand wird als Kreis dargestellt
- mögliche Zustandsübergange als Pfeile dargestellt
- jeder Pfeil mit zugehörigem Eingabesymbol $a_m \in A$
	- abgetrennt mit einem "/" kann jeweils noch das Ausgabesymbol $b_n \in B$ angegeben werden

## Beispiel der Ampel
$a_0 = 0 \rightarrow$ Ampelknopf wurde nicht gedrückt
$a_1 = 1 \rightarrow$ Ampelknopf wurde gedrückt
- Anfangszustand $s_0 \in S$: Ampel grün
- Bei Knopfdruck zuerst Gelb werden, dann rot
- $a_1$ wechselt nach genügend Zeit automatisch zu $a_0$
- Ampel soll zunächst gelb-rot zeigen, dann wieder grün
- $A = \{ a_0, a_1 \}$ binär kodiert mit $\{0, 1\}$
- $S = \{ s_0, s_1, s_2, s_3\}$
- $B = \{b_0, b_1, b_2, b_3\}$ binär kodiert mit $y_2y_1y_0$
![[AmpelZustandsautomat.png|300]]

## Vom Zustandsdiagramm zur sequentiellen Schaltung

![[Vom Zustandsdiagramm zur sequentiellen Schaltung.png|400]]
