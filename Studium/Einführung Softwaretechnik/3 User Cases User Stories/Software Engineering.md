---
tags: Uni EST
VL-Date: 24.04.23
---
# [[Grundbegriffe]]
## Geschichte des Software Engineerings
Schon in den Sechzigerjahren bemerkte George Moore, Chef der Firma Intel, dass sich die Integrationsdichte etwa alle 18 Monate verdoppelt, also exponentiell wächst. Ähnlich entwickeln sich die Prozessorleistung und die Speicherkapazität pro €. Damit entstand der Eindruck, dass die Hardware-Entwicklung der Software davonläuft. Inwieweit Moore’s Law heute noch gilt ist diskussionswürdig. Aktuell kann man argumentieren, dass es noch gilt, falls man nicht nur einzelne Kerne betrachtet. Mit der Multicore-Technologie kann das Gesetz pro Prozessor noch als gültig angesehen werden.

In den Fünfzigerjahren war der Computer das schwächste Glied der Kette, und die Leistung der Programmierer wurde eingesetzt, um seine Unzulänglichkeiten zu kompensieren. Beispiel: Algorithmen, die trotz Hardware-Ausfällen ein korrektes Resultat lieferten. Bald aber waren diese Probleme überwunden, die Rechner wurden kleiner und billiger, schneller und zuverlässiger. Die Software wurde in dieser Zeit weder billiger noch zuverlässiger. Genauer: Die Kosten einer Zeile Code haben sich in Jahrzehnten kaum verändert. In höheren Sprachen leistet eine Zeile Code aber mehr als in den alten, primitiven Sprachen. Effekt: Die Software war von nun an der Schwachpunkt des Gesamtsystems.

Phänomen der späten Sechzigerjahre: Software-Projekte ließen sich selbst mit gigantischem Aufwand nicht zu einem befriedigenden Ende bringen (oder der Abschluss wurde nur mit schlechten Resultaten, viel zu spät und/oder mit extremen Kostenüberschreitungen erreicht). Gleichzeitig nahm die Bedeutung der Rechner laufend zu, so dass der Wunsch nach Methoden und Werkzeugen zur schnellen und billigen Entwicklung fehlerarmer Software immer drängender wurde. Für diese Probleme kam das Schlagwort „Software Crisis“ auf. Die Software-Krise war Anlass für viele Diskussionen und Tagungen.

Margaret Hamilton war die Leiterin des Software-Programms für die Apollo-Missionen. Ihr wird oft die Prägung des Begriffs „Software Engineering“ zugeschrieben. Video: https://youtu.be/kTn56jJW4zY

#### Beiträge der Frühzeit
- die „Entdeckung“ des Software Life Cycles (Royce, 1970)
- die Überlegungen zur Strukturierung der Programme (Parnas, 1972)
- die Sammlung empirischer Daten (Boehm et al., 1973) zum besseren Verständnis der Kosten-Ursachen und der Kosten-Verteilung

# Definition Software Engineering
Software Engineering ist die Entdeckung und Anwendung solider Ingenieur-Prinzipien mit dem Ziel, auf wirtschaftliche Art Software zu bekommen, die zuverlässig ist und auf realen Rechnern läuft. - F.L. Bauer

Software Engineering ist die Herstellung und Anwendung einer Software, wobei mehrere Personen beteiligt sind oder mehrere Versionen entstehen. - D.L. Parnas

### IEEE Definition
1. Systematic application of scientific and technological knowledge, methods, and experience to the design, implementation, testing and documentation of software. Übersetzt: Systematische Anwendung wissenschaftlichem und technologischen Wissens, Methoden und Erfahrung zum Design, Implementierung, Test und Dokumentation der Software.
2. Application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software; that is, the application of engineering to software. Übersetzt: Anwendung eines systematischen, disziplinierten, quantifizierbaren Ansatzes zur Entwicklung, Betrieb und Wartung von Software; kurz: die Anwendung von Ingenieursprinzipien auf Software.
Schwächen dieser Definition: An das Software Engineering werden Erwartungen geknüpft, die unrealistisch sind und in der Praxis kaum erfüllt werden. Eine Definition sollte nicht werten! Das Ingenieurwesen wird als Fundament verwendet, das leider selbst nicht (besser) definiert ist.

## gute Definition
Software Engineering ist jede Aktivität, bei der es um die Erstellung oder Veränderung von Software geht, soweit mit der Software Ziele verfolgt werden, die über die Software selbst hinausgehen. - Ludewig (2001)

## SE als globale Optimierung
Ziel: Wir wollen die Gesamtkosten senken. Ein Ansatz wäre, die einzelnen SE-Aktivitäten auf Möglichkeiten zur Einsparung abzuklopfen. Dieser naive Ansatz führt aber nicht zum Ziel, denn die Aktivitäten sind miteinander verknüpft. Wenn man sparen will, kann man die Spezifikation und den Architekturentwurf weglassen, wird dafür aber später, schon beim Test und bei der Integration, mehr noch in der Wartung, bestraft. Es ist also notwendig, das globale Optimum zu suchen. Dafür gibt es keine simple Formel! Wir müssen ein differenziertes Bild der Kosten und ihrer Beziehungen entwickeln, um uns dem Optimum zu nähern. Wir müssen dort, wo uns auch das differenzierte Bild der Kosten nicht weiterhilft, weil es zu viele Details bietet, nach dem Vorbild der Ingenieurinnen das Prinzip der hohen Qualität anwenden.

## SE als defensive Disziplin
Software Engineering spielt in der Informatik eine ähnliche Rolle wie die Hygiene in der Medizin: Sie nützt nichts, sondern verhindert vielmehr Schäden und sollte generell beachtet werden. Ist dieses Ideal erreicht, so ist sie als eigenständiges Fach überflüssig. Software Engineering ist – wie die Hygiene – langweilig und frustrierend für Leute, die die Abwehr von Fehlschlägen und Katastrophen nicht als positive Leistung betrachten.

## SE als ein Gestrüpp von Problemen
![[SE als ein Gestrüpp von Problemen.png|300]]

Eine Schwierigkeit ist die wechselseitige Verknüpfung zwischen den Maßnahmen, die zum Software Engineering gerechnet werden. Beispiel: Qualitätssicherung erfordert eine Konfigurationsverwaltung. Konfigurationsverwaltung setzt die Stabilität der Teilprodukte voraus, was nur durch Qualitätssicherung möglich ist.

__Software Engineering ist Technologie für die Köpfe__:
Wissenschaftliche Erkenntnis und neue Technologie lassen sich gut in die Anwendung transferieren, wenn sie sich in Produkten niederschlagen. Einen Compiler oder ein Betriebssystem kann man benutzen, ohne die Technik zu verstehen. Leider lassen sich die Fortschritte im Software Engineering nur zu einem kleinen Teil in Werkzeuge gießen. Häufig entstehen im Software Engineering Einsichten und Regeln, die von den SoftwareEntwicklerinnen umgesetzt werden müssen. Software Engineering zielt darauf ab, das Verhalten dieser Leute zu verändern. Nur, wenn den Entwicklern gute Arbeit, Beachtung der Normen, penible Prüfung usw. selbstverständlich sind, können wir erwarten, solide Produkte zu erhalten.

### [[Shu-Ha-Ri]]
[[Shu-Ha-Ri]] beschreibt den Lernprozess in japanischen Kampfsportarten. Man geht von shu (gehorchen) zu ha (abweichen) zu ri (separieren). Anfangs sollte man also die Techniken direkt so nachahmen, wie es die Meister vorgeben. Fortgeschrittene Anwenderinnen können anfangen von den Vorgaben abzuweichen. Erst wenn man selbst Meisterin ist, sollte man sich ganz von den Vorgaben lösen. Ich sehe hier eine starke Analogie zum Software Engineering. Viel zu oft werden Methoden gar nicht erst so eingesetzt, wie eigentlich vorgesehen und dann wird darüber geklagt, dass es nicht funktioniert. Deshalb sollte man auch im SE erstmal mit shu starten.