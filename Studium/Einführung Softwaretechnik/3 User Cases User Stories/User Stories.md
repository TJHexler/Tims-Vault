---
tags: Uni EST
VL-Date: 24.04.23
---
# User Stories und Definition of Done
Im Gegensatz zum traditionellen Verständnis einer Spezifikation wird bei User Storys nicht davon ausgegangen, dass die Anforderungen alle zum gleichen Zeitpunkt im Detail ausgearbeitet sein müssen. Stattdessen gibt es zu Beginn grobe Backlog Items, die erst mit der Zeit und je nach Priorität detailliert werden. Man nennt das die fortschreitende Verfeinerung (Progressive Refinement). Dies stellt sicher, dass immer nur der jeweils notwendige Aufwand in die Anforderungsbeschreibung gesteckt wird und nicht etwa Anforderungen im Detail aufgearbeitet werden, die später gar nicht mehr umgesetzt werden. Im Gegensatz zur oft vertretenen Auffassung bedeutet dies nicht, dass keine oder nur grobe Anforderungen definiert werden. Hierzu wird eine sehr flexible Spezifikationsmethode benötigt, in der seht grobe, aber auch detaillierte Anforderungen beschrieben werden können.

#### warum grobe Granularität am Anfang
- geringstes Wissen am Anfang
- Aufwand für nicht umgesetzte Anforderungen
- große Änderungskosten
- wenige Gespräche, da Anforderungen "fertig"
Rubin (2013) diskutiert die angegebenen Nachteile, wenn am Anfang alle Anforderungen auf die gleiche (niedrige) Granularitäts-Ebene spezifiziert werden. Im Gegensatz fordert er die über das Projekt fortschreitende Verfeinerung durch Gespräche (Conversations) der Stakeholder zum jeweiligen Zeitpunkt, an der die Detaillierung für die Verwendung im Sprint benötigt wird.

## User Stories
![[UserStorieKarteBeispiel.png|300]]

Hier sehen wir eine Story Card, was eine typische Art der Dokumentation einer User Story darstellt. Wir haben für jede User Story einen Namen, meist eine ID, eine Beschreibung und eine Aufwandsbeschreibung. Die Beschreibung besteht aus „As a“, einem Rollennamen, „I want to“, einer Aktion der Rolle, „so that“ und einem entsprechenden Kontext bzw. Zusatzbedingungen. 

### Die 3 C's
__Card, Conversation, Confirmation__
„Card“ ist das erste „C“ der drei Cs, die nach Jeffries (2001) User Stories beschreiben. Das zweite ist „Conversation“. Damit ist gemeint, dass eine User Story niemals im Detail bereits die Anforderung festschreibt, sondern ein „Merker“ zur weiteren Konversation mit den Stakeholdern sein soll.

### [[Akzeptanztests]]
Das dritte C ist „Confirmation“. Das bedeutet, dass wir auf der Rückseite der Story Card Informationen angeben, wie die Erfüllung der User Story zu überprüfen ist. Oft werden diese „Conditions of Satisfaction“ genannt. Häufig formuliert man diese direkt als [[Akzeptanztests]], also [[Tests]], die der Kunde ausführt, um zu prüfen, ob das System abgenommen werden kann. Dazu gibt es auch entsprechende Werkzeuge, wie z.B. FitNesse, das solche tabellarisch formulierten Tests direkt ausführen kann.

![[AkzeptanztestsGliederung.png|350]]

Wir nutzen unterschiedliche Ebenen der Detaillierung. In einer frühen Phase des Projekts, in der wir nur den Product Backlog (eine spezielle Form der Spezifikation) aufbauen, werden wir sehr grobgranulare Storys aufschreiben. Diese werden oft „Epics“ genannt. Sie sind bei weitem zu groß, um sie in einem Sprint zu bearbeiten, dienen aber als Platzhalter für weitere Verfeinerungen. Features brechen Epics herunter, sind aber immer noch zu groß für einen Sprint. Deshalb werden sie wiederum auf „Sprintable Stories“ oder „Implementable Stories“ verfeinert. Während der Umsetzung definieren wir dann mehrere Tasks für jede Sprintable Story.

## Definition of Done
![[DefinitionOfDone.png|200]]

Die „Definition of Done“, also die Definition wann man fertig ist, ist ein wichtiges Konzept, das wir auch in der Anforderungsdefinition gebrauchen können.

## Nichtfunktionale Anforderungen
Nichtfunktionale Anforderungen können direkt in die Definition of Done einfließen. Damit stellt man sicher, dass sie in jedem Sprint überprüft werden. Alternativ lassen sich dafür auch User Stories erstellen. Dies kann in der Schreibweise mit einer Rolle geschehen. Beispielsweise bei Security-Anforderungen passt das auch sehr gut. Falls es aber seltsam zu formulieren wäre, sind auch klassische Anforderungsformulierungen akzeptabel.
#### Beispiele
- System supports Safari 5 and Chrome 15.
- Code in standard format
- Code is commented
- Code contains no FindBugs warnings
- System can handle over 100 users
- User data connot be read by adversary

