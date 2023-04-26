---
tags: Uni Syskon
---
# Das Snapshot-Problem
Erstellung eines "Snapshots" des globalen Zustands, ohne System zu unterbrechen (Bsp.: Wie viel Geld ist im Umlauf)
--> niemand hat globale Perspektive, können System nicht einfrieren
## Snapshot Algorithmus von Chandy und Lamport
erster Algorithmus 1985 veröffentlicht
##### Ziel
- Aufzeichnung einer Menge von Prozess- und Kanalzuständen für eine Menge von Prozessen $p_i$ (i = 1, 2, ..., N), sodass aufgezeichneter globale Zustand konsistent ist, obwohl aufgezeichnete (lokale) Zustände nie gleichzeitig ausgeführt wurden
##### Algorithmus
- zeichnet (Prozess- und Kanal-)Zustand lokal in den Prozessen auf
- beinhaltet keine Methode um globalen Zustand an einem bestimmten Ort zu erfahren
- offensichtliche Methode: Prozesse senden den aufgezeichneten Status zum Sammlerprozess
##### Annahmen
- weder Kanäle noch Prozesse schlagen fehl
- zuverlässige Kommunikation (jede Nachricht wird genau 1 mal erhalten)
- Kanäle sind unidirektional und bieten FIFP-geordnete Nachrichtenaustellung
- der Graph von Prozessen und Kanälen ist stark miteinander verbunden (es gibt einen Pfad zwischen jeden zwei beliebigen Prozessen)
- jeder Prozess kann zu jeder Zeit einen Snapshot initiieren
- Prozesse können weiter ausgeführt werden und normal Nachrichten senden und erhalten während der Snapshot erstellt wird
##### Modell
- unidirektionale Kanäle
- FIFO-geordnete Zustellung
- Eingehend: Kanäle, über die Prozesse Nachrichten erhalten
- Ausgehend: Kanäle, zum Senden
- Graph von Prozessen und Kanälen ist stark verknüpft
##### Ziel
- __konsistenter Schnitt__: verhindert Nachrichten "aus der Zukunft" (m1)
- Nachrichten im Transit (m2 wurde in grauen Epoche gesendet und wird in blauer Epoche empfangen)
- nicht in aufgezeichneten Prozessstatus des Empfängers abgebildet
- sollen im Kanalzustand aufgezeichnet werden
- ![[Snapshot Problem.png]]
##### grundlegende Idee
- jeder Prozess zeichnet folgende Informationen auf
	- Prozesszustand
	- Nachrichten, die ihm zugesendet wurden
- welche Nachrichten werden aufgezeichnet?: Für jeden der in p eingehenden Kanäle, jede Nachricht,
	- die empfangen wird, nachdem p seinen Zustand aufgezeichnet hat
	- die gesendet wurde, bevor der Sender seinen eigenen Zustand aufgezeichnet hat
##### Marker
- Algorithmus verwendet spezielle Marker-Nachrichten mit 2 Aufgaben:
	- Aufforderung an Empfänger, Zustand aufzeichnen
	- bestimmt welche Nachrichten in Kanalzustand kommen
- Algorithmus durch 2 Regeln definiert:
	- die Marker Empfangsregel für Prozess $p_i$ über Kanal c erhalten: 
		if ($p_i$ Zustand noch nicht aufgezeichnet)
			zeichne Prozesszustand auf;
			zeichne Zustand von c als leere Menge auf;
			starte Nachrichtenaufzeichnung, die über andere Kanäle empfangen werden
		else
			$p_i$ zeichnet Zustand von c als Menge von Nachrichten, die er über c empfangen hat, auf, da dieser Kanal seinen Zustand speichert
	- die Marker-Senderegel für Prozess $p_i$
		für jeden ausgehenden Kanal c, nachdem $p_i$ seinen Zustand aufgezeichnet hat, sendet $p_i$ eine Markernachricht über c(bevor irgendwelchen anderen Nachrichten)
##### Anmerkung
- Senderegel zwingt Marker zu senden nach Aufzeichnung, aber bevor irgendwelchen anderen Nachrichten
- Empfangsregel zwingt Aufzeichnung und Markierung eingehender Marken, falls erster Marker, sonst Nachrichten aufzeichnen (Bsp. Kanalzustand)
- Jeder Prozess kann Algorithmus zu beliebiger Zeit beginnen --> Empfangsregel abarbeiten
- verschiedene Prozesse können Algorithmus starten --> Marker müssen unterschieden werden können
##### Bsp. 1
![[Snapshot Bsp. 1.png]]
##### Bsp. 2
![[Snapshot Bsp. 2.png]]
##### Bsp. 3
![[Snapshot Bsp. 3.png]]
Vorsicht: Austausch von Nachrichten abhängig von Topologie
