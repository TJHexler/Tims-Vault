---
tags: Uni Syskon
---
# Zeit und globaler Zustand
#### Motivation
Reihenfolge von Events, Zeitvergleiche bestimmen Reigenfolge --> ABER: es gibt keine universelle (globale) Zeit
#### Physische Uhren
$a_i(t)*t + b_i(t) = C_i(t)$
- $a_i(t)$ unterschiedliche Zeitraten $C_i$ (drift) zur Zeit $t$
- $b_i(t)$ unterschied beim Lesen der Uhrzeit $C_i$ (skew) zur Zeit $t$
Computeruhren:
- unterschiedliche Zeit-Raten Periode
- typische Drift Rate: $c = 10^{-5}$ relativer Fehler
Ideal: $dC_i(t)/dt = 1$ (schnelle Uhr: $dC_i(t)/dt > 1$)
#### Synchronisation
Konfigurationen:
- Computer hat Referenzuhr (Radio-Uhr) vs. kein Computer hat Referenzuhr
Ziele:
- Uhrensynchronisation mit externer Zeitquelle vs. Uhrensynchronisation ohne externe Zeitquelle (interne Synchronisation)
#### Basics
$|dC_i(t)/dt -1| <= c$
- c max Driftrate
- $C_i,C_k$ synchronisiert bei $t_0$
- $t_1 = t_0 +  ∆t$ ist erfüllt mit $|C_i(t_1) - C_k(t_1)| <= 2c * ∆t$
#### Methoden
Lamport 1978:
- Prozesse tauschen periodisch Informationen aus
- verteilter Ansatz
- es gibt keine Referenzzeit
Cristian 1989
- Prozesse synchronisieren Zeit periodisch mit __"Master Server"__
- Synchronisation mit der Referenzzeit
### Cristian's Algorithmus
Berechnen der Umlaufzeit einer Nachricht $R = (T_1 - T_0) - (T_3 - T_2), d = R/2$
![[Umlaufzeit einer Nachricht Cristian Algorithmus.png]]
- $P_i$ erhält die Uhr von $C_m$ vom Master Server $(C_i(T_1) := C_m + d); C_m$ gelesen zur Zeit $T_3$
- wenn $C_i > C_m + d$ verlangsame $C_i$, setze Uhr __niemals__ zurück!
- periodische Anfrage an Master wünschenswert
### Physische Uhren
- messen Zeiteinheiten
- erlauben Reihenfolge von Ereignissen (Zeitstempel, synchronisierte Uhren erforderlich)
- oft genügt kausale Abhängigkeit --> keine Echtzeitabhängigkeit
- bildet "Ursache vor Effekt" ab
## Prinzip der Kausalität
Wenn ein Event x in irgendeiner Weise die Ursache für ein zweites Event y ist --> x hat vor y stattgefunden (Bsp.: Senden vor Empfangen)
Anwendungen:
- Identifikation eines globalen einheitlichen Zustands
- zuverlässiger, geordneter [[Multicast]]
- kausale Konsistenz
## Logische Uhren Lamport 1978 Systemmodell
[[Verteilte Systeme]]:
- Menge von Prozessen
- Prozesskommunikation durch Nachrichten
- Prozesse werden als Abfolge von Events gebildet
- Events:
	- Senden oder Empfangen, lokale Ausführung einer Prozedur, Prozessanweisung, Datenbankzugriff, etc.
## "Happend Before" Definition
[[Relation]] "happend-before" (-->) auf einer Event-Menge ist kleinste [[Relation]] mit: a, b Events eines Prozesses:
a vor b: a --> b
wenn a senden und b dazugehöriges Empfangen: a --> b
__Transitivität__: a-->b und b-->c: a-->c
zwei Events a, b heißen __parallel__ oder __kausal unabhängig__ (a||b), wenn weder a-->b noch b-->a gilt
"-->"definiert Halbordnung auf Event-Menge
## Lamport Uhren
logische Uhren = jeder Prozess $P_i$ hat Uhr $C_i: e -> N; e Event in P_i$
Uhrensystem = Funktion C ordnet jedem Event e eine Zahl $C(e)$ zu mit $C(e) = C_i(e)$, e Event in $P_i$
![[Lamport Uhren.png]]
Uhrensystemkorrekt, wenn für alle $a,b: a-->b => C(a) < C(b)$(__Uhrenbedingung__)
Uhrenbedingung erfüllt wenn 
1. für alle $a,b: a-->b => C(a) < C(b)$
2. a Sende-Event in $P_i$ und b dazugehöriges Empfangen in $P_k => C_i(a) < C_k(b)$
jeder Prozess $P_i$ verwaltet seine lokale hr $C_i$
Initialisierung: $C_i := 0$
lokales Event: $C_i := C_i + 1$
Sende Event: $C_i := C_i + 1; T_m := C_i$ send(m, $T_m$)
Empfangs Event: receive(m',$T_{m'}); C_i := max(C_i, T_{m'}) + 1$
![[Lamport Uhren Empfangs Evente.png]]
Umkehrung der Uhrenbedingung gilt nicht: $C(a) < C(b) !=> a-->b$
Es gilt: $C(a) < C(b) => a-->b oder a||b; C(a) < C(b) => !(b-->a)$
__starke Uhrenbedingung__ a-->b $<=>$ C(a) < C(b)
## Vektor Uhren (Mattern 1989)
Lamport's Uhrenbedingung reicht nicht für ableiten von kausalen Abhängigkeiten aus logischen Uhren
Vektor Uhren beinhalten das Äquivalent eines Zeitstempels sowie einer logischen  Abhängigkeit über Prozesse hinweg: VC(a) < VC(b) $<=>$ a-->b
Zeitstempel ist n-dimensionaler Vektor
Zeit ist Menge dieser Vektoren 
eine Uhr ist ein array c(1:n)
- VC($p_i$)(k) = k-te Komponente der Vektor Uhr des Prozess $p_i$
- VC(a) = Zeitstempel des Events a
- VC(a)(k) = k-te Komponente des Zeitstempels
![[Vektoruhren.png]]
### kausale Abfolge von Events
![[kausale Abfolge von Events.png]]
VC(e)(i) = Anzahl Events, die e kausal voranstehen
VC(e) kodiert die kausale Vergangenheit
### Vektoruhren Arithmetik
![[Vektoruhren Arithmetik.png]]
### Algorithmus
- analog zur Lamport Uhr, unter Verwendung von Vektoren --> Supremum der Vektoren
![[Vektoruhren Algorithmus.png]]
Bsp.:
![[Vektoruhren Beispiel.png]]
### Anwendungen
- Grundlagen vieler verteilter Algorithmen (Broadcast, Termination; DeadLock-Erkennung, Garbage-Collection, etc.)
- generell fast überall verwendet, wo konsistente Zustands-Informationen in [[verteilte Systeme]]n aufgezeichnet werden müssen
## verteilte Terminierung
Wann sind [[verteilte Systeme]] in Ruhe? --> verteilte Berechnung fertig --> Ergebnisauslieferung oder keine Nachrichten mehr --> Protokoll/System kann aktualisiert werden
Systemmodell: keine globale Ansicht, Nachrichtenlaufzeiten
unterschiedliche Ansätze: __[[Kreditmethode]]__ oder Doppelzählverfahren
## Zusammenfassung
- Uhren sind wichtig in [[verteilte Systeme]]
	- Koordination (Event Korrelation)
	- Messungen
- unterschiedliche Anforderungen führen zu unterschiedlichen "Uhren" z.B.: 
	- logische Uhren 
	- physische Uhren
- viele Aufgaben werden in verteilten Systemen kompliziert, z.B.:
	- Terminierung
	- Reference Counting
	- [[Snapshot]]s