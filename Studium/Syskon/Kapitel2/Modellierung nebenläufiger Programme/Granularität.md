---
tags: Uni Syskon
---
# atomare Befehle
- Programmiersprachen fassen mehrere elementare Operationen zusammen --> atomare Befehle nicht intuitiv auf Ebene einer Programmiersprache erkennbar
- werden **vollständig ohne Unterbrechung** ausgeführt
	- keine Verschachtelungen mit anderen Befehlen
	- Befehl wird ganz oder gar nicht ausgeführt
- ob Befehle atomar sind, erfordert Wissen über
	- [[Abbildung]] der Befehle auf Maschinenbefehle des Rechners
	- Kenntnis über Ausführung der Befehle auf der Maschine

# unterschiedliche granularität möglich
- atomizität auf verschiedenen Ebenen sichergestellt: Hardware, Systemebene, Übersetzer, Programmiersprache
## falsche Granularitätsannahme
- welche Sequenz von Befehlen wird als atomare Einheit betrachtet und zu einem "Ausführungsschritt" zusammengefasst
- inkorrekte (nebenläufige) [[Programmausführung]] möglich!

Bsp.: 
	![[Programm Print each number once.png]]
	--> erfordert Atomizität von p2 und q2 (Granularität auf Ebene einer Zeile)
	--> keine Atomizität von p2 und q2 ermöglichen weitere Verschachtelungen
	![[Programm print each number once Atomare Befehle.png]]
	--> mögliche Wertepaare($x_p, x_q$): (1,1) (1,2) (2,1) (2,2)
Beachte: jeder Prozess hat eigenen Stapel
	- Registermaschine: jeder Prozess hat eigene Kopie der Register, auch bei Ein-CPU-Maschinen

# Granularität von Atomitizität
grundsätzlich gilt: Atomare Ausführung eines Befehls = Befehl verwendet maximal einen Lese- oder Schreib-Zugriff auf gemeinsamen Speicher

Anmerkung Java: Schlüsselwort **volatile** --> atomare Lese- oder Schreib-Zugriffe