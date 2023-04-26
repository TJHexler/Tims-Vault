---
tags: Uni Syskon
---
# Scheduling
![[Prozesszustände Schedulingzeiten.png]]
## warum langfristiges Scheduling?
Hinzufügen eines neuen Prozess würde zu vorhersehbaren Problemen mit bestehenden Prozessen führen
---> Ablehnung des neuen Prozess
Bsp.: __Echtzeit-Scheduling__: n Prozesse garantieren Echtzeiteigenschaften (alle Deadlines werden eingehalten)
neuer Prozess --> __Einplanungstest__ --> garantierte Echtzeiteigenschaften mit n + 1 Prozessen?
	Ja: lasse neuen Prozess zu
	Nein: lehne neuen Prozess ab
## warum mittelfristiges Scheduling?
Beobachtung: je mehr Prozess, desto effizientere E/A Ausnutzung
zu viele Prozesse und wenig Hauptspeicher --> häufiges Ein-/Auslagern von Speicherseiten auf Festplatte
Suspendierung von Prozessen um restliche Prozesse effizienter ablaufen zu lassen
## warum kurzfristiges Scheduling?
__Entscheidet welche Prozesse/[[Threads]] auf dem Prozessor ablaufen__
unterschiedliche Verfahren für Uniprozessor, Multiprozessor, Echtzeitsystem
wichtige Kriterien für Algorithmen:
- schneller Kontextwechsel
- schnelle Entscheidung in der Auswahl des Prozesses

## Uniprozessor-Scheduling
Verfahren hängt von Anforderungen ab (Auslastung, Durchsatz, Antwortzeiten, Durchlaufzeit, [[Fairness]])
Prozess kann zwischen zwei Phasen wechseln: __CPU Burst__ und __I/O-Burst__
Je nachdem, was häufiger ausgeführt wird, ist der Prozess __Prozessorlastig__ oder __E/A-lastig__
Schedulingverfahren sind entweder __nicht präemptiv__ oder __präemptiv__
### nicht präemptiv
aktiver Prozess führt bis zur Blockierung bzw. Terminierung aus
--> keine Uhren-[[Unterbrechungsbehandlung]]
häufig fpr Batch-Systeme verwendet
Ziele von Batch-Jobs: hohe Prozessorauslastung, kurze durchschnittliche Antwortzeit(hoher Durchsatz)
Verfahren:
- FIFO
- SPN (shortest Process next)(Prozesse mit kürzestem CPU-Burst zuerst)
Problem: __Aushungern__ (niedrige Prio führt niemals aus) sowohl für FIFP als auch bei SPN möglich
--> Lebendigkeit in nebenläufiger Programmierung erfordert [[Fairness]]!
### präemptiv
aktiver Prozess kann unterbrochen werden (auch wenn er noch bereit ist) 
--> begrenzt Ausführungszeit eines Prozesses
nötig für __interaktive Anwendungen__
Ziele interaktiver Anwendungen: Jeder Prozess gute Antwortzeit, [[Fairness]] in Ausführung
Verfahren: __Round Robin__(jeder Prozess erhält Zeitscheibe der Prozessorzeit)

## FIFO
__Priorität__ eines Prozesses: Wartezeit in Beireitwarteschlange
Implementierung: kurze Kontextwechsel durch verkettete Liste (einfach .poll() in der queue)
--> Positiv: geringer Aufwand für Scheduler
--> Negativ: Prozesse mit langen CPU-Burst behindern Prozesse mit kurzen --> viele Prozesse warten in Bereitwarteschlange
--> ungünstig für Durchsatz (nicht nebenläufig, aber warten auf E/A geschiegt nebenläufig)

## SPN
__Priorität__ eines Prozesses: Länge des CPU-Bursts
Implementierung: 
1. Prioritätswarteschlange (z.B. Min-Heap) --> höhere Kosten für Kontextwechsel
2. länge des nächsten CPU-Bursts (in Praxis schätzen aufgrund Länge vorangegangener CPU-Bursts)

## Vergleich FIFO und SPN
bei FIFO hält ein langsamer Prozess alle anderen Prozesse lange auf
SPN minimiert __durchschnittliche Antwortzeit__ und __maximiert Durchsatz__ (Beweisbar optimal für nicht-präemptiv)

## Round Robin
aktive Prozesse erhalten zusätzliches maximales Zeitquantum
Implementierung: Scheduler initialisiert Uhren-[[Unterbrechungsbehandlung]]
--> anders als bei FIFO oder SPN existiert Übergang __aktiv__ --> __bereit__
Zeitquantum entscheidet über Scheduling:
- großes Quantum --> Verhalten ähnlich zu FIFO
- kleines Quantum --> hoher Aufwand durch häufige Kontextwechsel(in Praxis 10 - 100 ms)
### mehrere Bereitwarteschlangen
führt zur effizienten Auswahl
Zeitquanten in oberen Warteschlangen kleiner
manchmal unterste Bereitqueue FCFS
![[mehrere Bereitwarteschlangen Round Robin.png]]
### Scheduling mit statischen Prioritäten
Prioritätenbereiche für Klassen (z.B. Echtzeit, Kern, interaktiv)
pro Prio eine Warteschlange --> Scheduling-Policy (z.B. RR, FIFO) definiert Prozess Position innerhalb Warteschlange
### Scheduling Policies
SCHED_OTHER: 
	Completely Fair Scheduler:
	- dynamische Prio aufgrund Wartezeit
	- Präemption nach max. Ausführungszeit
	- nice Level +- 20: beeinflusst CPU Zeit
SCHED_BATCH:
	Scheduler geht immer von CPU intensivem Prozess aus
	Prozess wird leicht benachteiligt
SCHED_IDLE:
	niedrigste Priorität
### erweiterte Problemstellung
Uniprozessor-System --> eindimensionales Problem, wann soll Prozess (oder Thread) ausgeführt werden= --> Uniprozessor-Scheduling-Algorithmen
Multiprozessor-System --> zweidimensionales Problem, wann und wo Prozessausführung? --> nicht Klausurrelevant WS22/23 :)

