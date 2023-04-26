---
tags: Uni Syskon
---
# Unterschied Programm und Prozess
Programm:
- Abfolge von Befehlen
	- Speicher (Variablen, Konstanten) lesen/schreiben
	- Berechnungen (Addition, Multiplikation, Bitoperation, etc.)
	- Sprunganweisung (bedingte Sprünge, Schleifen, etc.)
- Befehle aus Sicht der Rechnerarchitektur: Maschinenbefehle
	- typischerweise werden Befehle der Programmiersprache in mehrere Maschinenbefehle übersetzt
	--> [[Unterbrechungsbehandlung]] des Programms zwischen Maschinenbefehlen
Prozess:
- Programm + Zustand
- Programm-Befehle werden in den Hauptspeicher geladen und ausgeführt
- Zustand:
	- Programmdaten (globale und statische Variablen)
	- Ausführungskontext, v.a. folgende Prozessorregister:
	- Programmzähler: Adresse des aktuellen oder nächsten Befehl
	- allg. Prozessorregister: Daten für Berechnungen
	- Statusregister: Übertragsflag, zero-Flag, etc.
	- Stack-Zeiger: lokale Variablen, Funktionsparameter, etc.
- Laden und Speichern von Prozesszuständen passiert durch [[Betriebssystem]], das selber ein Programm ist (privilegiertes Programm, entzieht und übergibt Prozessen Kontrolle über CPU)