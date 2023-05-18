---
tags: Uni EST
VL-Date: 08.05.23
---
# Akzeptanztest
Manchmal ist es schwierig den Unterschied zwischen Akzeptanz- und Systemtests herauszuarbeiten. Akzeptanztests sind klar aus Sicht der Kunden und Anwender. Sie sollten direkten Bezug zu den entsprechenden Nutzeranforderungen im Sinne von Funktionalität und Features haben. Systemtests testen weitere Aspekte der [[Integration]] von Funktionalität im Gesamtsystem, oft in einer möglichst realen Umgebung. Insbesondere werden hier nichtfunktionale Aspekte, wie Performanz oder Sicherheit getestet.

1. Testing conducted to determine whether a system satisfies its acceptance criteria and to enable the customer to determine whether to accept the system.
2. Formal testing conducted to enable a user, customer, or other authorized entity to determine whether to accept a system or component.

## Akzeptanztestgetriebene Entwicklung
User Story auswählen $\rightarrow$ Identifiziere Akzeptanzkriterien $\rightarrow$ Implementiere Akzeptanztest $\rightarrow$ Fehlschlagende Akzeptanztests $\rightarrow$ Implementierung $\rightarrow$ Bestandener Akzeptanztest $\rightarrow$ Test refactoren / Akzeptanz durch Kunden $\rightarrow$ User Story auswählen

In der Akzeptanztest-getriebenen Entwicklung nehmen wir die Akzeptanztests, typischerweise auf Systemebene, als Grundlage für die ganzen weiteren Entwicklungsaktivitäten. Wir leiten aus der Anforderung – meist in Form einer User Story – Akzeptanzkriterien ab, wie wir es in der Anforderungsanalyse bereits kennengelernt haben. Dies sind meist Beispiele oder Beispielszenarien. Diese formulieren und implementieren wir dann in einem automatisierten Akzeptanztest. Dieser schlägt erst einmal fehl. Wir bauen die passende Implementierung, bis der Akzeptanztest bestanden wird. Wir schließen die Sache mit einem Aufräumen des [[Tests]] und der Akzeptanz durch den Kunden (oder Product Owner) ab.

### Beispiel: fitnesse.org
FitNesse (fitnesse.org) ist eins der ersten Werkzeuge, die Akzeptanztest-getriebene Entwicklung (AGE) unterstützten. Es ist auch heute noch in Verwendung und setzt die wesentlichen Teile von AGE um. Es verwendet ein Wiki-System, um die Akzeptanztests in Form von Tabellen zu beschreiben. Diese Tabellen verbindet es dann mit sogenannten Fixtures, die man als Entwickler schreiben muss, um die Testdaten an das System zu schicken und die Ausgaben zurück ins Wiki zu bringen.

## verhaltensgetriebene Entwicklung (Behaviour-Driven Development BDD)
BDD ist eine spezielle Form und in gewissem Sinn eine Weiterentwicklung der akzeptanztestgetriebenen Entwicklung. Der Fokus rückt etwas vom Testen weg, obwohl weiterhin automatisiert ausgeführte Tests dahinter stecken. Stattdessen spricht man wieder mehr von der Spezifikation des Verhaltens. Das Ziel ist es, eine Form dafür zu wählen, die auch von Nicht-Softwareexperten verstanden werden kann. Das Beispiel auf der Folie benutzt die Sprache Gherkin dazu. Sie kann im Cucumber-Framework verwendet werden. Siehe auch: https://www.youtube.com/watch?v=VS6EEUVZGLE&t=162s

## Muster: Common Includes
- Problem: viele Tests sehen ähnlich aus, da sie erst die Umgebung für den Test aufbauen müssen. Das erzeugt unnötige Mehrarbeit beim Schreiben und Ändern.
- Lösung: Gemeinsamkeiten werden an eine Stelle herausgezogen und dann in den Test eingebunden
## Muster: Parameterized Includes
- Problem: viele Tests sehen ähnlich aus, da sie die gleich oder ähnliche Funktionalität nur mit anderen Parametern prüfen. Das erzeugt unnötige Mehrarbeit beim Schreiben und Ändern
- Lösung: In die Tests werden Parameter integriert, die mit separat spezifizierten Werten belegt werden können.
## Antimuster: Creating Scenarios by Domain Experts or Developers in Isolation
- Symptom: Die Tests werden nicht im Three Amigos Meeting diskutiert, sondern die Domänen-Experten oder die Entwickler bauen die Szenarien alleine auf.
- Problem: Dadurch entsteht kein gemeinsames Verständnis der Anforderungen an die Software. Wenn Domänenexperten alleine Szenarien entwickeln, fehlt die technische Expertise und die Tests sind schwerer zu automatisieren. Wenn Entwickler alleine an Szenarien arbeiten, dann entsprechen sie nicht den eigentlichen Nutzerbedürfnissen.
Der Einsatz von Gehring und Cucumber oder ähnlicher Frameworks ist allein durch Entwickler nötig. Viele Befürworter von BDD betonen aber, dass auch das sogenannte Three Amigos Meeting ein integraler Bestandteil von BDD ist. Damit ist gemeint, dass wann immer eine User Story bearbeitet werden soll, sich ein Domänenexperte, ein Entwickler und ein Tester zusammensetzen, um gemeinsam die Szenarien zu entwickeln und ihre drei Sichtweisen dabei einfließen zu lassen. Für ein Beispiel siehe https://www.youtube.com/watch?v=M238SpxRtqA

