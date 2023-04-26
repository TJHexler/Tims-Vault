---
tags: Uni Syskon
---
# Die Kreditmethode
- basiert auf globalen Invariante (credit c)
- für jede Summe aller Kredite c gilt immer __c = 1__
- jede Delegationsnachricht hat einen Kredit > 0
- Kredit wird mit Ergebnis zurückgegeben
- jeder Prozess $p_i$ hat Kredit c($p_i$) mit $p_i$ = 0 if $p_i$ is passive, c($p_i$) > 0 if $p_i$ is active
- System in Ruhe __(quiscent)__ wenn Initiatorprozess $p^*$ Kredit c($p^*$) = 1 wieder hat --> keine ausstehenden Aufgaben mehr
##### Ansatz
1. $p^*$ startet verteilte Berechnung mit c($p^*$) = 1
2. für jede Delegationsnachricht verschickt $p^*$ Hälfte seines Kredits
3. bei $p^l$ erhalt von $p_i$, erhöht sich c($p^l$) um den Wert der Nachricht ($p^l$) wird nun aktiv
4. wird Prozess passiv, sendet er seinen Kredit an $p^*$
##### Bsp.
![[Kreditmethode Bsp.png]]
- Fließkommaarithmetik ungenau --> __Kreditanteile werden durch Exponent der Basis 2 angezeigt__
- local integer CREDIT --> c($p_i$) = $2^{-Credit}
## Sending activation message
CREDIT := CREDIT + 1; --> halbieren
send(CREDIT, msg) to $p_i$; --> sende andere Hälfte
## receiving activation message
- bei Erhalt von Nachricht mit credit share CR bei $p_i$, CR wird $p^*$ übergeben, wenn $p_i$ bereits aktiv
- sonst wird $p_i$ aktiv und c($p_i$) = CR - if (active) send(CR) to $p^*$
- else active = true; CREDIT = CR
## returning Credit
- send(CREDIT) to $p^*$D; active = false;
## Debt Collection
- $p^*$ hat dynamisches Set __DEBTS__ (integer) mit D = Summe aller Debts
- Initial: D = 1
- $p^*$ ehält credit share --> D := D - $2^{-CR}$
- System ruht bei D == 0 --> Fließkommazahlen... --> Initial: D = {1}, bei Erhalt:
![[Debt Collection Kreditmethode.png]]
### Bsp.
![[Kreditmethode Debt Collection Bsp.png]]
## Limitierung
- Algorithmus kann mehrere Nachrichten von $p^*$ nicht unterscheiden
- somit kann es dazu kommen, dass $p^*$ zwei Berechnungen startet und zwischenzeitlich alle Credits wieder bekommt, obwohl das System nicht quiscent ist
- ABER: $p^*$ weiß, wenn Berechnungen initiiert und sequentialisiert werden