---
tags: Uni EST
VL-Date: 18.04.23
---
# Frage des Tages
Was ist der Unterschied zwischen Lastenheft und Pflichtenheft?

# Analyse und Spezifikation

| Grundlagen               | Aktivitäten                                               |
| ------------------------ | --------------------------------------------------------- |
| [[Grundbegriffe]]            | Analyse und Spezifikationen                               |
| [[Software Engineering]]     | Kollaborationswerkzeuge Integration Test                  |
| Software-Qualität        | Programmverstehen und Implementierung, Qualitätssicherung |
| Risiko, Vorgehensmodelle | Produkt-/Projektmanagement                                |
| langlebige Software      | Architektur und Entwurf                                   |

# Was ist Anforderungsanalyse
##### Lernziele
- Wissen zur Bandbreite der Anforderungsanalyse
- Verstehen der Definitionen von Anforderungen und Anforderungsanalyse
##
Die Anforderungen der Kund*innen an die Software sind die wichtigsten Informationen in einem Software-Projekt.
Die Kundin erwartet, dass ihr die Software über einen gewissen Zeitraum hinweg als williger und billiger Diener zur Verfügung steht, ihr also bestimmte Leistungen erbringt, ohne von ihr umgekehrt erhebliche Leistungen (in Form von Kosten, Aufwand, Mühe, Arger) zu fordern. Die Software soll ihr dienen, nicht umgekehrt.
Werden die Erwartungen, die Anforderungen der Kund*in, nicht vollständig und präzise erfasst, ist damit zu rechnen, dass das entwickelte Produkt die Anforderungen nicht (vollständig) erfüllt.
Die vollständige und präzise Erfassung der Anforderungen ist eine wichtige Voraussetzung für eine erfolgreiche Software-Entwicklung.
### Anforderungsanalyse ist abhängig von der Kundendomäne
Software wird heute in allen Bereichen des Lebens und der Wirtschaft verwendet. Wir bezeichnen diese verschiedenen Bereiche als Anwendungsdomänen. Die Anwendungsdomäne beeinflusst viele Aspekte der Entwicklung einer Software. Zum Beispiel kommt in der Entwicklung von Steuerungssoftware von Maschinen und Motoren oft die Sprache C zum Einsatz, während für große Web-Systeme eher Java, C# oder JavaScript verwendet wird.
Die Anforderungsanalyse hängt vielleicht am stärksten von der Domäne und dem weiteren Kontext (z.B. der Art und Größe des Unternehmens der Entwickler und der Kunden) ab. In regulierten Domänen, wie dem Flugzeugbau, finden wir sehr detaillierte, umfangreiche textuelle Anforderungsspezifikationen, die evtl. mit graphischen Modellen ergänzt sind. Bei einem einfachen Smartphone-Spiel, werden hingegen wahrscheinlich nur ganz grobe textuelle Anforderungen festgehalten. Bei Banken müssen bestimmte Gesetze mit eingehalten werden. Bei großen Organisationen fest bürokratische Wege beschritten werden.
## Anforderungsanalyse Schritte
1. Studieren der Verbraucher-Needs, um eine Definition von System, Hardware oder Software-Anforderungen festzulegen
2. Verfeinerung der festgelegten Anforderungen
3. Systematische Untersuchung der User-Requirements, um ein System zu definieren
4.  Determination of product- or service-specific performance and functional characteristics based on analyses of customer needs, expectations, and constraints; operational concept; projected utilization environments for people, products, services, and processes; and measures of effectiveness.
## Requirement
1. Statement that translates or expresses a need and its associated constraints and conditions
2. Condition or capability that must be met or possessed by a system, system component, product, or service to satisfy an agreement, standard, specification, or other formally imposed documents.
3. Provision that contains criteria to be fulfilled.
4. A condition or capability that must be present in a product, service, or result to satisfy a contract or other formally imposed specification.
## Funktional vs. nicht-funktional
Funktion der Software = Beziehung zwischen Ein- und Ausgaben, im weiteren Sinne auch das Zeitverhalten

Alle Anforderungen, die sich auf diese Funktion beziehen, sind __funktionale Anforderungen__, alle anderen sind __nichtfunktionale Anforderungen__ (==non-functional requirements, NFRs==). Achtung, das Wort „*funktional*“ ist mehrdeutig!

Die Abgrenzung funktional – nichtfunktional ist unscharf.
Anforderungen, die zwar die Funktion betreffen, aber nicht präzise formuliert werden können, werden vielfach als nichtfunktional eingeordnet. Beispiele: Robustheit, Bedienbarkeit.
Auch das Zeitverhalten wird meist als NFR behandelt. Viele nichtfunktionale Anforderungen werden funktional, wenn man sie weit genug herunter bricht. Beispielsweise ist „Die Datenübertragung zwischen den Komponenten soll vor Angreifer*innen* geschützt sein.“ eine nichtfunktionale Anforderung. Bei genauerer Spezifikation ist es aber eine funktionale Anforderung: „Die Datenübertragung verwendet HTTPS.“

Funktionale und nichtfunktionale Anforderungen werden gebraucht. Praktisch alle Aussagen zur Wartbarkeit („Das System muss leicht portierbar sein.“) sind nichtfunktional.

### Studie zu nichtfunktionalen Anforderungen von Eckhardt, Vogelsang und Mendez Fernandez
![[Studie zu nichtfunktionalen Anforderungen von Eckhardt, Vogelsang und Mendez Fernandez.png|350]]

In dieser Studie wurden 530 nichtfunktionale Anforderungen aus industriellen Anforderungsspezifikationen klassifiziert. Viele dieser Anforderungen sind aber gar nicht eindeutig „nicht-funktional“. Ein starker Anteil lässt sich dem Typ „Funktionalität“ zuordnen. Dies zeigt, dass auch in der praktischen Anwendung die Aufteilung nicht immer klar ist.

##
Glinz hat eine mögliche Klassifikation der Anforderungen vorgestellt. Er teilt im Gegensatz zur funktional/nicht-funktionalen Unterscheidung auf oberster Ebene in Anforderungen an das Projekt, an das System und an den Prozess auf. Die Systemanforderungen können dann funktionale Anforderungen, Attribute oder Randbedingungen (Constraints) sein. Randbedingungen sind nicht weiter zu begründende Festlegungen innerhalb eines Unternehmens (z.B. Verwendung der MySQLDatenbank). Attribute beinhalten dann Qualitäts- und Performanzanforderungen, wobei man Performanz auch als eine Qualität sehen könnte.
![[Glinz on Nonfunctional requirements.png|350]]

## Software Anforderungs-Spezifikationen (SRS)
1. Dokumentation der essenziellen Anforderungen (function, performance, design constraints, attributes) der Software und ihrer external interfaces.
2. Strukturierte Ansammlung der Anforderungen (functions, performance, design constraints und attributes) der Software und ihrer external interfaces.
![[Software Requirements Speifikation.png|350]]
So vielfältig wie die Anforderungsanalyse sind dann auch Spezifikationen in der Praxis. Sie kann aus einer Reihe von „Merkern“ bestehen, die nur daran erinnern, dass man diese Punkte noch genauer diskutieren muss, bevor man sie umsetzt. Sie kann aber auch eine sehr detaillierte Vorgabe sein, was in einem Software-Projekt umgesetzt werden muss. Es gibt viele schlechte Spezifikationen; oft gibt es gar keine. Die Spezifikation ist aber ein zentrales Artefakt im Projekt. Es ist notwendig für eine ganze Reihe von wichtigen Aspekten.

## Lastenheft vs Pflichtenheft
| Lastenheft        | Pflichtenheft |
| ----------------- | ------------- |
| Problemorientiert | Konkret       |
| Abstrakt          | Präzise       |
|                   | konsistent    |
|                   | abgestimmt    |
|                   | vollständig   |
|                   | messbar       |

Vor der Erteilung eines Auftrags, muss folgendes festgelegt werden: 
- Was soll das System leisten? 
-  Welche Qualitätseigenschaften soll das System haben? (Zusätzliche Forderungen) 
- Welche Kosten entstehen bei der Entwicklung des Systems?
Der Auftraggeber erstellt dafür zunächst ein Lastenheft (oder Anforderungssammlung):
- Beschreibung aller Anforderungen aus Sicht des Auftraggebers 
- Das Lastenheft ist Bestandteil der Ausschreibung
Der potentielle Auftragnehmer erstellt eine Leistungsbeschreibung und schließlich ein Pflichtenheft (oder Anforderungsspezifikation): 
- Konkretisierung aller im Lastenheft enthaltenen Anforderungen 
- Enthält auch eine Beschreibung der angestrebten Lösungsansätze 
- Pflichtenheft ist Vertragsbestandteil bei der Auftragsvergabe

# Ablauf der Anforderungsanalyse und -spezifikation
##### Lernziele
- Verstehen des allgemeinen Vorgehens zur Anforderungsanalyse
## 
Das Ziel der Analyse ist es, den Soll-Zustand festzustellen. Idealerweise müsste es also reichen, die Kund*innen* und Nutzer*innen* nach ihren Wünschen zu fragen. Aber: Sie konzentrieren sich auf das, was ihnen derzeit nicht gefällt. Wir sind also bei jeder Umstellung auf die Schwachpunkte des bestehenden Systems fixiert; seine Stärken nehmen wir erst wahr, wenn sie uns fehlen. Implizit erwarten die Nutzer*innen*, dass alles, was bisher akzeptabel oder gut war, unverändert bleibt oder besser wird. Die Anforderungen an das neue System bestehen also nur zum kleinsten Teil aus Änderungswünschen, die allermeisten Anforderungen gehen in Richtung Kontinuität. Darum hat die Ist-Analyse, also die Feststellung des bestehenden Zustands, große Bedeutung für die erfolgreiche Projektdurchführung. Bei Widersprüchen ist der Ist-Zustand zudem ein sicherer Halt!

![[Der Prozess zur Spezifikation der Anforderungen nach Pfleeger und Atlee (2010).png|350]]

Es beschreibt also stärker die Soll-Analyse als die Ist-Analyse. Letztere ist wahrscheinlich stärker unter „Sammeln“ zu sehen.

## Anforderungsquellen
![[Quellen für mögliche Anforderungen basierend auf Robertson und Robertson (1999).png|350]]

In der Analyse sollten alle zur Verfügung stehenden Daten und Dokumente ausgewertet werden. Auf dieser Basis werden typischerweise Befragungen durchgeführt. Wo möglich und nötig können auch Beobachtungen der existierenden Prozesse durchgeführt werden.

In der Befragung sollte eine Mischung aus geschlossenen und offenen Fragen verwendet werden. Durch Befragungen in der Form von Interviews können mehr Details erfahren werden, durch Fragebögen werden mehr Menschen erreicht. Eine spezielle Form des Interviews, in der die Stakeholder gut eingebunden werden können sind Story-Writing Workshops. Wenn noch weitergehende Fragen beantwortet werden müssen, die früh geklärt werden müssen, dann können Modelle des Systems oder Prototypen gebaut bzw. Experimente durchgeführt werden.

![[Analysetechnik zielt ab auf.png|350]]

### Befragungen
- offene Fragen: Auf welchen Endgeräten wollen Sie das System benutzen? vs. Wollen Sie das System über den Browser benutzen?
- anfangs möglichst kontextfreie Fragen: Wer sind die Nutzer? Welche anderen Stakeholder werden von dem neuen System betroffen sein?

Befragung muss gut geplant sein. Die Interviewer sollten sich vorab einen Leitfaden für die Befragung schreiben, um nichts zu vergessen. Außerdem muss klar sein, wer die Antworten wie festhält. Deshalb empfiehlt es sich meist zwei Interviewer einzusetzen, um sich die Aufgaben zu teilen. Bei einer schriftlichen Umfrage müssen die Fragen zwangsweise spezifischer und geschlossener sein, da sonst die Auswertung extrem aufwändig wird. Aber auch dort sollte man einige offene Fragen stellen, um wirklich alle Aspekte einzusammeln.

### Story-Writing Workshop
- Nutzerrollen und/oder Personas identifizieren
- Papier/Whiteboard-Prototypen der Nutzerschnittstelle
- Fragen stellen: Was wird der Nutzer wahrscheinlich als nächstes tun wollen? Welche Fehler könnte der Nutzer hier machen?
- Ideen in Form von initialen User Storys festhalten

Eine Möglichkeit zum sammeln und analysieren von Anforderungen ist es, an einem Termin (ein bis zwei Tage), alle Beteiligten (Kunden, Nutzer, Entwickler) zusammenzubringen, um sogn. User Storys zu schreiben. Eine User Story nimmt sehr knapp eine Anforderung aus Nutzer*innen*-Sicht auf. Im Workshop kann man verschiedene Methoden, wie Brainstorming oder Papier-Prototypen, verwenden.

### Personas
Personas beschreiben vollkommen fiktive aber realistische Personen, die Nutzer*innen* des Systems repräsentieren. Sie können genutzt werden, um sich bei der Anforderungsanalyse leichter in die Nutzer*innen* hineinversetzen zu können und damit für sie passende Anforderungen zu identifizieren. Dabei werden wirklich detaillierte Vorstellungen der Personen entworfen und mit Bildern versehen. Diese können im Story-Writing Workshop oder auch bei anderen Analysemethoden verwendet werden.

## 
Es gibt leider nur begrenzte empirische Evidenz zur Anforderungsanalyse, weil empirische Studien relativ kompliziert sind. Davies et al. (2006) haben den damaligen Stand in einem systematischen Review zusammengeführt. Dort hatten strukturierte Interviews Evidenz, dass sie die effektivste Form der Anforderungserhebung sind.

Laut Umfragen werden Interviews am häufigsten verwendet. Daraus kann man folgern, dass auch Praktiker*innen* auch Interviews als effektivste Methode einschätzen. 

## Das Analysieren
Laut Sommerville (2007):
Analysieren: Klassifizieren und organisieren $\rightarrow$ Priorisieren und verhandeln $\rightarrow$ Dokumentieren

- Klassifizierung und Organisation der Anforderungen: Hierbei wird die unstrukturierte Sammlung von Anforderungen mit verwandten Anforderungen gruppiert und somit in zusammenhängende Gruppen zusammengefasst. 
- Priorisierung und Verhandlung von Anforderungen: Wenn viele Projektbeteiligte involviert sind, kommt es unausweichlich zu Konflikten bei den Anforderungen. Diese werden in diesem Schritt durch Verhandlungen zwischen den Stakeholdern aufgelöst. Zusätzlich werden die Anforderungen in der Diskussion mit den Stakeholdern priorisiert, um herauszufinden, welche Anforderungen zwingend (Muss-Anforderungen) und welche zusätzlich (Soll- und Kann-Anforderungen) sind. 
- Dokumentation der Anforderungen: Die Anforderungen werden genauer beschrieben. Dies ist der Übergang zum nächsten großen Schritt, dem Spezifizieren.

## Das Spezifizieren
Es gibt eine sehr große Bandbreite an Methoden, die man zur Spezifikation von Anforderungen verwenden kann. Die dargestellten Methoden sind nicht orthogonal. Nicht für alle Systeme ist jede Methode sinnvoll und effizient.
![[Spezifikationsmethoden.png|350]]

Die Methode, die in der Praxis am häufigsten verwendet wird sind Texte und strukturierte Texte. In vielen Fällen könnten diese textuellen Spezifikationen aber gewinnbringend durch andere Methoden ergänzt werden, um das Verständnis zu erleichtern und präziser zu spezifizieren.

### 7 wichtige Merkmale einer Anforderungsspezifikation
- __Adäquat__: beschreibt das, was der Kunde will bzw. braucht
- __vollständigkeit__: beschreibt alles, was der Kunde will bzw. braucht
- __Widerspruchsfrei__: sonst ist die Spezifikation nicht realisierbar
- __verständlich für alle Beteiligten__: auch für nicht-Techniker und nicht-Domänen-Experten lesbar
- __eindeutig__: vermeidet Fehler durch Fehlinterpretationen
- __prüfbar__: man kann feststellen, ob das System die Anforderung erfüllt
- __risikogerecht__: Umfang umgekehrt proportional zum Risiko, das man eingehen will

### Die INVEST-Regel

- __I__ ndependent
- __N__ egotiable
- __V__ aluable
- __E__ stimatable
- __S__ ized Appropriately
- __T__ estable

Wake (2003) hat das Akronym INVEST geprägt. Spezifizierte Anforderungen sollen also möglichst unabhängig sein, um die Auswahl für die Abarbeitung zu erleichtern. Sie sollen nicht so viel vorwegnehmen, dass es im Gespräch mit den Stakeholdern nicht mehr möglich ist, sie zu verfeinern. Sie sollen für den Kunden oder den Nutzer wertvoll sein. Sie sollen für den Anforderungsanalysten, den Produktmanager und das Team abschätzbar sein. Sie sollen (für ihre jeweilige Detaillierungsebene) angemessen groß sein. Sie sollen testbar sein (also gute Akzeptanzkriterien definieren). Nur mit prüfbaren Anforderungen können wir am Ende wirklich beantworten, ob das System die Anforderungen erfüllt. Dies ist eine rechtliche Frage, aber auch ein Punkt, der den Entwicklern Sicherheit geben kann. Weiterhin hängt damit die Überprüfung nicht so stark vom Prüfer ab. Die Prüfung wird zuverlässiger (vgl. Metriken).

## Frage des Tages
Wie schätzen Sie die folgende Anforderung anhand der INVEST-Kriterien ein? 
- Die Waren im Warenkorb sollen bei der Bezahlung mit Kreditkarte, Überweisung oder Paypal bezahlt werden können.

## Begriffslexikon
| Steuergerät          | eingebettetes System                                                                                                                                  |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ein Steuergerät ist die physische Umsetzung eines eingebetteten Systems. | Ein eingebettetes System ist eine Software/Hardware-Einheit, die über Sensoren und Aktuatoren mit einem Gesamtsystem verbunden ist und darin Überwachungs-, Steuerungs- bzw. Regelungsaufgaben übernimmt. |

## Standard-Gliederung

![[standardgliederung einer SRS laut IEEE.png|300]]

Die IEEE schlägt eine Gliederung für Anforderungsspezifikationen vor, die häufig zum Vorbild für Spezifikationen in der Praxis genommen wird. Teil 1 steckt den Rahmen der Spezifikation ab, beinhaltet das Begriffslexikon und Verweise auf andere Dokumente (z.B. relevante Standards). Teil 2 gibt dann einen allgemeinen Überblick über das System, seine Einbettung in die Umgebung sowie die wichtigsten funktionalen und weiteren Anforderungen. Teil 3 spezifiziert dann die Einzelanforderungen. Diese können unterschiedlich strukturiert sein. Er muss die folgenden Informationen enthalten:
- funktionale Anforderungen
- Qualitätsanforderungen
- Leistungsanforderungen
- Einschränkungen des Entwurfs
- Definition der externen Schnittstellen zu anderen Systemen

![[Pasted image 20230418142808.png|350]]

Teil 3 der Spezifikation kann bestehen aus:
- Systembetriebsmodi
- Objekten
- Features
- Stimulus, Reaktion
- funktionaler Hierarchie

## Das Validieren
Die Anforderungen zu validieren bedeutet, dass wir mit den Stakeholdern die spezifizierten Anforderungen prüfen. Dies kann durch ein gemeinsames Durchsprechen oder detaillierte Reviews realisiert werden. Auch die Implementierung von Prototypen ist eine Form der Validierung. Zum Beispiel könnte man eine stark vereinfachte Version der Benutzeroberfläche bauen, die potentielle Nutzer verwenden und Rückmeldung geben.