---
tags: Uni Syskon
---
# Fairness
betrachte Lebendigkeitseigenschaft "Jede Anfrage wird schließlich beantwortet"
Problem: Es können unendliche Folgen entstehen und manche Prozesse bzw. [[Threads]] verhungern
Voraussetzung für Lebendigkeit: Jeder Befehl wird letztendlich ausgeführt

## schwache Fairness
- schwache Fairness garantiert keine schließliche Ausführung von Befehlen
- lange aber endliche Folge von Befehlen möglich
Bsp.:
	get_Request()
	--> nur Ausführungsbereit, wenn Anfrage gestellt wurde
	--> nicht **ständig ausführungsbereit**

### Definition 2.5
Eine schwach faire Ausführung eines Programms garantiert, dass jeder ständig ausführungsbereite Befehl eines Prozesses schließlich ausgeführt wird.

## starke Fairness
- starke Fairness garantiert bei unendlich vielen Anfragen unendlich viele Ausführungen
- aufwendiger zu implementieren
### Definition 2.5
Eine stark faire Ausführung eines Programms garantiert, dass jeder unendlich oft (nicht notwendigerweise ständig) ausführungsbereite Befehl eines Prozesses unendlich oft ausgeführt wird.